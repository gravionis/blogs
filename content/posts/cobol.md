+++
date = '2025-01-30T10:00:00+00:00'
draft = false
title = 'COBOL Guide'
tags = ['COBOL', 'Mainframe', 'Business Programming', 'Legacy Systems',]
+++

COBOL (Common Business-Oriented Language) is a high-level programming language created for business data processing, especially on mainframes. It is known for its English-like syntax and is widely used in industries such as banking, insurance, and government for batch and transaction processing. This guide provides an overview of COBOL, its features, structure, and key concepts, helping developers understand and work with COBOL programs, especially in the context of mainframe systems.

## Table of Contents
- [What is COBOL?](#what-is-cobol)
- [Key Features](#key-features)
- [COBOL vs Java](#cobol-vs-java)
- [Mainframe Context & File Types](#mainframe-context--file-types)
- [Basic Structure of a COBOL Program](#basic-structure-of-a-cobol-program)
  - [IDENTIFICATION DIVISION](#identification-division)
  - [ENVIRONMENT DIVISION](#environment-division)
    - [CONFIGURATION SECTION](#configuration-section)
    - [INPUT-OUTPUT SECTION](#input-output-section)
  - [DATA DIVISION](#data-division)
    - [FILE SECTION](#file-section)
    - [WORKING-STORAGE SECTION](#working-storage-section)
    - [LOCAL-STORAGE SECTION](#local-storage-section)
    - [LINKAGE SECTION](#linkage-section)
  - [PROCEDURE DIVISION](#procedure-division)
- [Key Concepts & Terminology](#key-concepts--terminology)
- [COBOL Data Types & Variables](#cobol-data-types--variables)
- [File I/O in COBOL](#file-io-in-cobol)
- [Copybooks](#copybooks)
- [JCL (Job Control Language)](#jcl-job-control-language)
- [Datasets](#datasets)
- [Utilities](#utilities)
- [Migration Tips for Java/Python/JS Developers](#migration-tips-for-javapythonjs-developers)
- [Getting Started](#getting-started)
- [Useful Resources](#useful-resources)

## What is COBOL?
COBOL (Common Business-Oriented Language) is a high-level programming language designed for business data processing, especially on mainframes. It is widely used in banking, insurance, and government systems for batch and transaction processing.

## Key Features
- **English-like Syntax:** COBOL code is verbose and reads like English, making it easy to understand.
- **Procedural Language:** COBOL is primarily procedural, focusing on step-by-step instructions.
- **Strong Data Processing:** Excellent for handling large volumes of data and batch processing.
- **Legacy Systems:** Many critical systems still run on COBOL, especially on mainframes.

## COBOL vs Java
| Aspect         | COBOL                          | Java                  |
|----------------|-------------------------------|-----------------------|
| Syntax         | Verbose, English-like          | Concise, C-like       |
| Paradigm       | Procedural                    | Object-Oriented       |
| Platform       | Mainframes, legacy systems     | Cross-platform (JVM)  |
| Use Cases      | Business, finance, batch jobs  | Web, mobile, desktop  |

## Mainframe Context & File Types

- **COBOL Programs**:
  - Source code files (`.cob`, `.cbl`) written in COBOL containing business logic and data processing. Comparable to `.java` or `.py` files. 
- **Copybooks**:
  - Reusable code or data structure snippets (`.cpy`), included in COBOL programs using the `COPY` statement. Analogous to Java imports or Python modules, often used for shared data definitions (e.g., record layouts).
- **JCL Scripts**:
  - Job Control Language files (`.jcl`) are Scripts used to run and schedule COBOL programs on mainframes. JCL is similar to shell scripts or Windows batch files, controlling program execution, input/output files, and job sequencing.
- **Datasets**: 
  - Files or databases on the mainframe, used to store input/output data. Datasets can be sequential files (like CSVs), VSAM files (indexed), or DB2 tables (relational). Analogous to files or SQL tables in Java applications.
- **Utilities**: 
  - System tools or programs for common tasks such as file copying, sorting, or data conversion. Examples include `IEBGENER` (copy files), `SORT` (sort data), and `IDCAMS` (manage VSAM datasets). These are similar to Unix command-line utilities like `cp`, `sort`, or `awk`.

---

## Basic Structure of a COBOL Program

A COBOL program is divided into four main divisions, each with specific sections or subsections:

- **IDENTIFICATION DIVISION**
  - Contains program metadata (name, author, etc.).
  - (no sections) Program metadata (name, author, etc.)
- **ENVIRONMENT DIVISION**
  - Specifies system/environment settings, such as file assignments.
  - Types of sections:
    - CONFIGURATION SECTION: System-dependent settings (SOURCE-COMPUTER, SPECIAL-NAMES)
    - INPUT-OUTPUT SECTION: File assignments and control (FILE-CONTROL, I-O-CONTROL)
- **DATA DIVISION**
  - Defines data structures and files used in the program.
  - Types of sections:
    - FILE SECTION: File record layouts
    - WORKING-STORAGE SECTION: Program variables (persistent for program duration)
    - LOCAL-STORAGE SECTION: Variables with local scope (reset on each call)
    - LINKAGE SECTION: Data passed from other programs or calling routines
- **PROCEDURE DIVISION**
  - Contains the executable logic (similar to Java methods/main).
  - (no sections) Executable program logic

### Example: PAYROLL-REPORT COBOL Program

```cobol
       IDENTIFICATION DIVISION.
       PROGRAM-ID. PAYROLL-REPORT.
       AUTHOR. Jane Doe.

       ENVIRONMENT DIVISION.
       CONFIGURATION SECTION.
           SOURCE-COMPUTER. IBM-370.
           OBJECT-COMPUTER. IBM-370.
           SPECIAL-NAMES. CONSOLE IS SYSIN.
       INPUT-OUTPUT SECTION.
           FILE-CONTROL.
               SELECT EMP-IN ASSIGN TO 'employee_input.txt'.
               SELECT EMP-OUT ASSIGN TO 'employee_output.txt'.

       DATA DIVISION.
       FILE SECTION.
       FD  EMP-IN.
       01  EMP-IN-REC.
           05 EMP-ID         PIC 9(5).
           05 EMP-NAME       PIC X(20).
           05 EMP-SALARY     PIC 9(6)V99.
           05 EMP-TAX        PIC 9(4)V99.
       FD  EMP-OUT.
       01  EMP-OUT-REC.
           05 EMP-ID-OUT     PIC 9(5).
           05 EMP-NAME-OUT   PIC X(20).
           05 NET-PAY        PIC 9(6)V99.

       WORKING-STORAGE SECTION.
       01  EMP-COUNT         PIC 9(4) VALUE 0.
       01  EOF-FLAG          PIC X VALUE 'N'.

       LOCAL-STORAGE SECTION.
       01  TEMP-NET-PAY      PIC 9(6)V99.

       LINKAGE SECTION.
       01  COMPANY-NAME      PIC X(30).

       PROCEDURE DIVISION USING COMPANY-NAME.
           DISPLAY 'Payroll Report for ' COMPANY-NAME
           OPEN INPUT EMP-IN
           OPEN OUTPUT EMP-OUT
           PERFORM UNTIL EOF-FLAG = 'Y'
               READ EMP-IN INTO EMP-IN-REC
                   AT END
                       MOVE 'Y' TO EOF-FLAG
                   NOT AT END
                       ADD 1 TO EMP-COUNT
                       COMPUTE TEMP-NET-PAY = EMP-SALARY - EMP-TAX
                       MOVE EMP-ID TO EMP-ID-OUT
                       MOVE EMP-NAME TO EMP-NAME-OUT
                       MOVE TEMP-NET-PAY TO NET-PAY
                       WRITE EMP-OUT-REC
               END-READ
           END-PERFORM
           CLOSE EMP-IN
           CLOSE EMP-OUT
           DISPLAY 'Processed ' EMP-COUNT ' employees.'
           STOP RUN.
```
---

## Key Concepts & Terminology
- **Mainframe Terms vs Java Terms**:
  | Mainframe/COBOL      | Java Equivalent                |
  |----------------------|-------------------------------|
  | Program (COBOL)      | Class or main method          |
  | Copybook             | Import/module/shared class     |
  | JCL                  | Shell script/Batch file       |
  | Dataset              | File/Database table           |
  | Utility (SORT, etc.) | Command-line tool/Library     |

- **Other Concepts**:
  - **Batch Processing**: COBOL is often used for batch jobs—processing large volumes of data in scheduled runs, similar to Java batch frameworks (e.g., Spring Batch).
  - **CICS**: Customer Information Control System, a transaction processing system for online COBOL programs (not covered in detail here).
  - **EJECT Directive**: A compiler directive used to start a new page in the source code listing for improved readability and organization. It does not affect program execution. Example usage:
  ```cobol
  EJECT
  * This section starts on a new page in the listing
  ```

---

## COBOL Keywords

In COBOL, keywords (reserved words) are predefined words that have special meaning to the compiler. You cannot use them as variable names or identifiers. They define structure, actions, or data descriptions. Here are the main categories of COBOL keywords, organized for clarity:

### 1. Program Structure Keywords
| Keyword                | Purpose                                         |
|------------------------|-------------------------------------------------|
| IDENTIFICATION DIVISION| Start of the program description.               |
| ENVIRONMENT DIVISION   | Specifies hardware and I/O environment.         |
| DATA DIVISION          | Defines variables, files, and data areas.       |
| PROCEDURE DIVISION     | Contains the actual program logic.              |
| PROGRAM-ID             | Declares program name.                          |
| SECTION                | Groups related paragraphs.                      |
| PARAGRAPH              | Defines a logical block of statements.          |
| STOP RUN               | Terminates the program.                         |
| EXIT PROGRAM           | Returns control from a subprogram.              |

### 2. Input/Output (I/O) Keywords
| Keyword      | Purpose                                                      |
|--------------|--------------------------------------------------------------|
| SELECT       | Declares a file for use.                                     |
| ASSIGN       | Associates file with external device (e.g., disk).           |
| FILE-CONTROL | Defines logical-to-physical file mapping.                    |
| OPEN         | Opens a file for processing (OPEN INPUT, OUTPUT, etc.).      |
| CLOSE        | Closes a file.                                               |
| READ         | Reads a record from a file.                                  |
| WRITE        | Writes a record to a file.                                   |
| REWRITE      | Updates an existing record.                                  |
| DELETE       | Deletes a record (in indexed files).                         |
| DISPLAY      | Outputs data to the screen or console.                       |
| ACCEPT       | Reads data from keyboard or system date/time.                |

### 3. Data Definition Keywords (used in DATA DIVISION)
| Keyword                | Purpose                                            |
|------------------------|----------------------------------------------------|
| FD                     | File Description entry.                            |
| WORKING-STORAGE SECTION| Defines program variables.                         |
| LINKAGE SECTION        | Parameters from calling programs.                  |
| PIC / PICTURE          | Defines data type/format.                          |
| VALUE                  | Assigns initial value.                             |
| OCCURS                 | Declares an array.                                 |
| REDEFINES              | Allows multiple layouts for same memory.           |
| COMP / COMP-3          | Binary / packed decimal storage.                   |
| FILLER                 | Unnamed data field (padding).                      |
| LEVEL NUMBER           | Hierarchical level indicator (e.g., 01, 05, 10).   |

### 4. Procedure/Logic Control Keywords
| Keyword      | Purpose                                                      |
|--------------|--------------------------------------------------------------|
| MOVE         | Assigns a value from one variable to another.                |
| ADD / SUBTRACT / MULTIPLY / DIVIDE | Arithmetic operations.                 |
| COMPUTE      | General arithmetic expression evaluation.                    |
| IF ... THEN ... ELSE | Conditional branching.                               |
| EVALUATE     | Multi-branch conditional (like switch in C).                 |
| PERFORM      | Executes a paragraph or section (loop or call).              |
| GO TO        | Transfers control (discouraged in modern COBOL).             |
| NEXT SENTENCE| Transfers control to next sentence.                          |
| STOP RUN     | Ends program execution.                                      |

### 5. String and Data Handling Keywords
| Keyword      | Purpose                                                      |
|--------------|--------------------------------------------------------------|
| STRING       | Concatenates multiple strings.                               |
| UNSTRING     | Splits a string into parts.                                  |
| INSPECT      | Examines or modifies strings (e.g., count, replace).         |
| INITIALIZE   | Resets data items to default values.                         |
| SET          | Assigns a value to index, condition, or pointer.             |

### 6. File and Record Control Modifiers
| Keyword      | Purpose                                                      |
|--------------|--------------------------------------------------------------|
| RECORD       | Defines a record structure.                                  |
| KEY IS       | Defines key field for indexed files.                         |
| ACCESS MODE  | Defines how file is accessed (SEQUENTIAL, RANDOM, etc.).     |
| ORGANIZATION | Defines file organization (e.g., LINE SEQUENTIAL, INDEXED).  |
| STATUS       | Captures file operation status codes.                        |

### 7. Conditions and Logical Keywords
| Keyword      | Purpose                                                      |
|--------------|--------------------------------------------------------------|
| NOT          | Logical negation.                                            |
| AND, OR      | Logical operators.                                           |
| IS           | Used in condition checks (IS EQUAL TO).                      |
| EQUAL, GREATER, LESS | Comparison operators.                                |
| ZERO, SPACES, HIGH-VALUES, LOW-VALUES | Predefined literals.                |
| TRUE, FALSE  | Boolean literals (not standard in all COBOL versions).       |

### 8. Declarative and Special Purpose Keywords
| Keyword      | Purpose                                                      |
|--------------|--------------------------------------------------------------|
| DECLARATIVES | Defines exception-handling routines.                         |
| END DECLARATIVES | Ends the declarative section.                            |
| USE AFTER ERROR | Error-handling trigger for file operations.               |
| COPY         | Includes external source code copybooks.                     |
| CALL         | Invokes another program.                                     |
| CANCEL       | Unloads a called program.                                    |
| EJECT        | Starts a new page in the source code listing.                |
| COMMENT      | Denotes a comment line (often with an asterisk `*` in column 7). |
| REMARK       | Another way to denote comments.                              |
| CONTINUE     | No operation; used in condition handling.                    |
| INITIALIZE   | Sets variables to default values.                            |
| RETURN       | Returns from a called program.                               |

## COBOL Data Types & Variables

- **Elementary Types**:
  - `PIC 9(n)`: Numeric (e.g., `PIC 9(5)` = 5-digit integer, like `int`).
  - `PIC X(n)`: Alphanumeric (e.g., `PIC X(10)` = 10-char string).
  - `PIC S9(n)V99`: Signed decimal with implied decimal (e.g., `S9(5)V99` = signed with 2 decimals).
- **Group Items**: Like structs or objects, grouping fields.
  ```cobol
  01 EMPLOYEE-REC.
     05 EMP-ID      PIC 9(5).
     05 EMP-NAME    PIC X(20).
  ```
- **Arrays**: `OCCURS` clause (like arrays/lists).
  ```cobol
  01 EMP-TABLE.
     05 EMP-REC OCCURS 10 TIMES.
        10 EMP-ID   PIC 9(5).
        10 EMP-NAME PIC X(20).
  ```

---

## File I/O in COBOL

- **File Declaration** (in ENVIRONMENT and DATA DIVISION):
  ```cobol
  ENVIRONMENT DIVISION.
  INPUT-OUTPUT SECTION.
  FILE-CONTROL.
      SELECT INFILE ASSIGN TO 'input.txt'.

  DATA DIVISION.
  FILE SECTION.
  FD  INFILE.
  01  IN-REC PIC X(100).
  ```
- **File Operations** (in PROCEDURE DIVISION):
  ```cobol
  OPEN INPUT INFILE
  READ INFILE INTO IN-REC
      AT END DISPLAY "EOF"
  CLOSE INFILE
  ```

---

## Copybooks

- **Purpose**: Share data layouts or code across programs.
- **Usage**:
  ```cobol
  COPY 'EMPLOYEE-REC'.
  ```
- **Analogy**: Like `import` in Python/Java, or `#include` in C.

---

## JCL (Job Control Language)

- **Purpose**: Run COBOL programs, define datasets, sequence jobs.
- **Example**:
  ```jcl
  //JOBNAME  JOB (ACCT),'DESC'
  //STEP1    EXEC PGM=SAMPLE-PROGRAM
  //INFILE   DD  DSN=INPUT.DATASET,DISP=SHR
  //OUTFILE  DD  DSN=OUTPUT.DATASET,DISP=NEW
  ```
- **Analogy**: Like a shell script or batch file that runs your program and manages files.

---

## Datasets

- **Sequential**: Like a text file or CSV.
- **VSAM**: Indexed files, like a key-value store.
- **DB2**: Relational database tables.

---

## Utilities

- **IEBGENER**: Copy files (like `cp`).
- **SORT**: Sort data (like Unix `sort`).
- **IDCAMS**: Manage VSAM datasets.

---

## Migration Tips for Java/Python/JS Developers

- **Data Types**: Map COBOL types to Java/Python types (`PIC 9(5)` → `int`, `PIC X(10)` → `String`).
- **Batch Logic**: COBOL batch jobs → Java (Spring Batch), Python (Pandas), JS (streams).
- **File I/O**: COBOL sequential files → Java `BufferedReader`, Python `open()`, JS file APIs.
- **Copybooks**: Convert to shared classes/modules.
- **JCL**: Replace with scripts, workflow tools, or job schedulers.
- **Testing**: Write unit tests to match COBOL output with new code.

---

## Getting Started

- **COBOL Compilers:** OpenCOBOL (GnuCOBOL), IBM COBOL.
- **Try Online:** [Online COBOL Compiler](https://www.tutorialspoint.com/compile_cobol_online.php)
- **Sample Project**: Start with a simple COBOL program, parse its structure, and try mapping it to Java/Python.

---

## Useful Resources
- [COBOL Programming Tutorials](https://www.tutorialspoint.com/cobol/index.htm)
- [GnuCOBOL Documentation](https://open-cobol.sourceforge.io/)
- [Java Migration Guides](https://www.oracle.com/java/technologies/migration.html)
- [Mainframe Modernization Patterns](https://cloud.google.com/architecture/mainframe-modernization)

## Sample Code: Employee Payroll Processing

This sample COBOL program demonstrates key constructs: all divisions, file I/O, group items, arrays, copybook usage, EJECT directive, and comments. The program reads employee data, calculates net pay, and writes results to an output file.

```cobol
       IDENTIFICATION DIVISION.
       PROGRAM-ID. PAYROLL-PROCESSOR.
       AUTHOR. GitHub Copilot.
       * Sample COBOL program for payroll processing

       ENVIRONMENT DIVISION.
       INPUT-OUTPUT SECTION.
       FILE-CONTROL.
           SELECT EMP-IN ASSIGN TO 'employee_input.txt'.
           SELECT EMP-OUT ASSIGN TO 'employee_output.txt'.

       DATA DIVISION.
       FILE SECTION.
       FD  EMP-IN.
       01  EMP-IN-REC.
           05 EMP-ID         PIC 9(5).
           05 EMP-NAME       PIC X(20).
           05 EMP-SALARY     PIC 9(6)V99.
           05 EMP-TAX        PIC 9(4)V99.

       FD  EMP-OUT.
       01  EMP-OUT-REC.
           05 EMP-ID-OUT     PIC 9(5).
           05 EMP-NAME-OUT   PIC X(20).
           05 NET-PAY        PIC 9(6)V99.

       WORKING-STORAGE SECTION.
       01  EMP-COUNT         PIC 9(4) VALUE 0.
       01  EOF-FLAG          PIC X VALUE 'N'.
       01  EMP-TABLE.
           05 EMP-ENTRY OCCURS 10 TIMES.
               10 EMP-ID-TBL     PIC 9(5).
               10 EMP-NAME-TBL   PIC X(20).
               10 EMP-SALARY-TBL PIC 9(6)V99.
               10 EMP-TAX-TBL    PIC 9(4)V99.
               10 NET-PAY-TBL    PIC 9(6)V99.

       * Simulated copybook usage
       COPY EMPLOYEE-REC REPLACING ==EMPLOYEE-REC== BY ==EMP-IN-REC==.

       PROCEDURE DIVISION.
           OPEN INPUT EMP-IN
           OPEN OUTPUT EMP-OUT
           PERFORM UNTIL EOF-FLAG = 'Y'
               READ EMP-IN INTO EMP-IN-REC
                   AT END
                       MOVE 'Y' TO EOF-FLAG
                   NOT AT END
                       ADD 1 TO EMP-COUNT
                       COMPUTE NET-PAY = EMP-SALARY - EMP-TAX
                       MOVE EMP-ID TO EMP-ID-OUT
                       MOVE EMP-NAME TO EMP-NAME-OUT
                       MOVE NET-PAY TO NET-PAY
                       WRITE EMP-OUT-REC
                       * Store in array for summary
                       MOVE EMP-ID TO EMP-ID-TBL(EMP-COUNT)
                       MOVE EMP-NAME TO EMP-NAME-TBL(EMP-COUNT)
                       MOVE EMP-SALARY TO EMP-SALARY-TBL(EMP-COUNT)
                       MOVE EMP-TAX TO EMP-TAX-TBL(EMP-COUNT)
                       MOVE NET-PAY TO NET-PAY-TBL(EMP-COUNT)
               END-READ
           END-PERFORM
           CLOSE EMP-IN
           CLOSE EMP-OUT

           EJECT
           * Print summary of processed employees
           DISPLAY 'Payroll Summary:'
           PERFORM VARYING IDX FROM 1 BY 1 UNTIL IDX > EMP-COUNT
               DISPLAY 'ID: ' EMP-ID-TBL(IDX) ' Name: ' EMP-NAME-TBL(IDX) ' Net Pay: ' NET-PAY-TBL(IDX)
           END-PERFORM
           STOP RUN.
```
