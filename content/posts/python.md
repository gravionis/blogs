+++
date = '2022-05-03T12:44:47+10:00'
draft = false
title = 'Python Quicky'
tags = ['Python']
+++

This guide covers all the essential Python topics you should master for technical interviews, from basic data types and control flow to advanced concepts like metaclasses, descriptors, and Python internals. It includes practical code examples, best practices, common pitfalls, and concise explanations to help you quickly revise and strengthen your understanding before interviews. Use this as a comprehensive checklist and reference to ensure you’re well-prepared for any Python interview scenario, whether for general programming, data science, web development, or system design roles.

## Table of Contents

- [1. Data Types & Structures](#1-data-types--structures)
  - [Basic Data Types](#basic-data-types)
  - [Collections](#collections)
  - [Time Complexity of Operations](#time-complexity-of-operations)
- [2. Control Flow & Functions](#2-control-flow--functions)
  - [Conditionals & Loops](#conditionals--loops)
  - [Functions](#functions)
- [3. Object-Oriented Programming](#3-object-oriented-programming)
  - [Classes and Inheritance](#classes-and-inheritance)
  - [Magic Methods (Dunder Methods)](#magic-methods-dunder-methods)
  - [Encapsulation and Properties](#encapsulation-and-properties)
- [4. Decorators](#4-decorators)
  - [Function Decorators](#function-decorators)
  - [Class Decorators](#class-decorators)
- [5. Iterators and Generators](#5-iterators-and-generators)
  - [Iterators](#iterators)
  - [Generators](#generators)
- [6. Exception Handling](#6-exception-handling)
- [7. Context Managers](#7-context-managers)
- [8. Memory Management & Garbage Collection](#8-memory-management--garbage-collection)
  - [Reference Counting](#reference-counting)
  - [Weak References](#weak-references)
- [9. Functional Programming](#9-functional-programming)
  - [Map, Filter, Reduce](#map-filter-reduce)
  - [Closures](#closures)
- [10. File Handling & I/O](#10-file-handling--io)
- [11. Modules and Packages](#11-modules-and-packages)
  - [Creating Modules](#creating-modules)
  - [Importing](#importing)
- [12. Regular Expressions](#12-regular-expressions)
- [13. Threading & Multiprocessing](#13-threading--multiprocessing)
  - [Threading](#threading)
  - [Multiprocessing](#multiprocessing)
- [14. Error Handling & Debugging](#14-error-handling--debugging)
  - [Exception Hierarchy](#exception-hierarchy)
  - [Debugging Techniques](#debugging-techniques)
- [15. Data Structures Implementation](#15-data-structures-implementation)
  - [Stack](#stack)
  - [Queue](#queue)
  - [Linked List](#linked-list)
- [16. Algorithms (Common Interview Questions)](#16-algorithms-common-interview-questions)
  - [Sorting](#sorting)
  - [Binary Search](#binary-search)
  - [Two Pointers Pattern](#two-pointers-pattern)
  - [Sliding Window](#sliding-window)
- [17. Dynamic Programming](#17-dynamic-programming)
  - [Memoization](#memoization)
  - [Classic DP Problems](#classic-dp-problems)
- [18. Built-in Functions & Libraries](#18-built-in-functions--libraries)
  - [Collections Module](#collections-module)
  - [Itertools](#itertools)
- [19. Common Gotchas & Best Practices](#19-common-gotchas--best-practices)
  - [Mutable Default Arguments](#mutable-default-arguments)
  - [Late Binding Closures](#late-binding-closures)
  - [Shallow vs Deep Copy](#shallow-vs-deep-copy)
- [20. Testing](#20-testing)
  - [Unit Testing](#unit-testing)
  - [Pytest (More Popular)](#pytest-more-popular)
- [21. Performance & Optimization](#21-performance--optimization)
  - [Timing Code](#timing-code)
  - [Memory Usage](#memory-usage)
- [22. Common Interview Questions & Patterns](#22-common-interview-questions--patterns)
  - [String Manipulation](#string-manipulation)
  - [Array Problems](#array-problems)
- [23. Metaclasses](#23-metaclasses)
  - [What is a metaclass? (`type` as the default metaclass)](#what-is-a-metaclass-type-as-the-default-metaclass)
  - [How to define and use a custom metaclass](#how-to-define-and-use-a-custom-metaclass)
  - [Typical use cases: enforcing class structure, auto-registering classes](#typical-use-cases-enforcing-class-structure-auto-registering-classes)
  - [Syntax for specifying a metaclass (`class Foo(metaclass=Meta): ...`)](#syntax-for-specifying-a-metaclass-class-foometaclassmeta-)
  - [When to use metaclasses vs. class decorators](#when-to-use-metaclasses-vs-class-decorators)
- [24. Descriptors](#24-descriptors)
  - [What is a descriptor? (`__get__`, `__set__`, `__delete__`)](#what-is-a-descriptor-get-set-delete)
  - [Difference between data and non-data descriptors](#difference-between-data-and-non-data-descriptors)
  - [How `property` works under the hood (uses descriptors)](#how-property-works-under-the-hood-uses-descriptors)
  - [Practical examples: validation, computed attributes](#practical-examples-validation-computed-attributes)
- [25. Advanced String Operations](#25-advanced-string-operations)
  - [String formatting: f-strings, `.format()`, `%` formatting](#string-formatting-f-strings-format-%-formatting)
  - [Unicode vs. bytes, encoding/decoding](#unicode-vs-bytes-encodingdecoding)
  - [String interning and its effect on memory/performance](#string-interning-and-its-effect-on-memoryperformance)
  - [Common pitfalls with string immutability](#common-pitfalls-with-string-immutability)
- [26. Python Internals](#26-python-internals)
  - [What is the GIL? How does it affect threading?](#what-is-the-gil-how-does-it-affect-threading)
  - [Python execution model: compilation to bytecode, interpretation](#python-execution-model-compilation-to-bytecode-interpretation)
  - [How to inspect bytecode with the `dis` module](#how-to-inspect-bytecode-with-the-dis-module)
  - [Impact of internals on performance and concurrency](#impact-of-internals-on-performance-and-concurrency)
- [27. Design Patterns](#27-design-patterns)
  - [Singleton, Factory, Observer patterns: implementation in Python](#singleton-factory-observer-patterns-implementation-in-python)
  - [When and why to use each pattern](#when-and-why-to-use-each-pattern)
  - [Pythonic alternatives (e.g., modules as singletons)](#pythonic-alternatives-eg-modules-as-singletons)
  - [Recognizing patterns in codebases](#recognizing-patterns-in-codebases)
- [28. Database Integration](#28-database-integration)
  - [Connecting to SQL databases with `sqlite3` or `psycopg2`](#connecting-to-sql-databases-with-sqlite3-or-psycopg2)
  - [Basics of SQLAlchemy ORM: models, sessions, queries](#basics-of-sqalchemy-orm-models-sessions-queries)
  - [Safe handling of database connections (context managers, pooling)](#safe-handling-of-database-connections-context-managers-pooling)
  - [Preventing SQL injection](#preventing-sql-injection)
- [29. Web Frameworks Basics](#29-web-frameworks-basics)
  - [Flask/Django: app structure, routing, request/response cycle](#flaskdjango-app-structure-routing-requestresponse-cycle)
  - [How to define and handle REST API endpoints](#how-to-define-and-handle-rest-api-endpoints)
  - [Basics of HTTP methods and status codes](#basics-of-http-methods-and-status-codes)
  - [Where to add authentication and validation](#where-to-add-authentication-and-validation)
- [30. Data Science Libraries](#30-data-science-libraries)
  - [NumPy: arrays, broadcasting, basic operations](#numpy-arrays-broadcasting-basic-operations)
  - [Pandas: DataFrame creation, indexing, filtering, groupby](#pandas-dataframe-creation-indexing-filtering-groupby)
  - [Data import/export (CSV, Excel, JSON)](#data-importexport-csv-excel-json)
  - [Common data manipulation patterns](#common-data-manipulation-patterns)
- [31. Networking & APIs](#31-networking--apis)
  - [Making HTTP requests with `requests` (GET, POST, headers, JSON)](#making-http-requests-with-requests-get-post-headers-json)
  - [Parsing and generating JSON](#parsing-and-generating-json)
  - [Basics of socket programming (TCP/UDP)](#basics-of-socket-programming-tcpudp)
  - [Error handling in network code](#error-handling-in-network-code)
- [32. Security Considerations](#32-security-considerations)
  - [Input validation and sanitization](#input-validation-and-sanitization)
  - [Common Python security pitfalls (e.g., `eval`, `pickle`)](#common-python-security-pitfalls-eg-eval-pickle)
  - [Safe file and database operations](#safe-file-and-database-operations)
  - [How to avoid code injection and insecure deserialization](#how-to-avoid-code-injection-and-insecure-deserialization)
- [33. Python 3 Features](#33-python-3-features)
  - [Type hints and annotations: syntax, benefits, `mypy`](#type-hints-and-annotations-syntax-benefits-mypy)
  - [Using `pathlib` for filesystem paths](#using-pathlib-for-filesystem-paths)
  - [F-strings and other modern syntax improvements](#f-strings-and-other-modern-syntax-improvements)
  - [Pattern matching (`match` statement, Python 3.10+): basic usage and caveats](#pattern-matching-match-statement-python-310-basic-usage-and-caveats)

## 1. Data Types & Structures

### Basic Data Types
```python
# Numbers
x = 42          # int
y = 3.14        # float
z = 2 + 3j      # complex

# Strings
s = "Hello"
s2 = 'World'
s3 = """Multi
line"""

# Boolean
flag = True
```

### Collections
```python
# Lists (mutable, ordered)
nums = [1, 2, 3]
nums.append(4)
nums.insert(0, 0)
nums.remove(2)

# Tuples (immutable, ordered)
coords = (10, 20)
x, y = coords  # tuple unpacking

# Sets (mutable, unordered, unique)
unique_nums = {1, 2, 3}
unique_nums.add(4)
unique_nums.discard(2)

# Dictionaries (mutable, ordered in Python 3.7+)
person = {"name": "Alice", "age": 30}
person["city"] = "NYC"
```

### Time Complexity of Operations
| Operation | List | Dict | Set | Tuple |
|-----------|------|------|-----|-------|
| Access | O(1) | O(1) | N/A | O(1) |
| Search | O(n) | O(1) | O(1) | O(n) |
| Insert | O(n) | O(1) | O(1) | N/A |
| Delete | O(n) | O(1) | O(1) | N/A |
| Append | O(1) | N/A | N/A | N/A |

## 2. Control Flow & Functions

### Conditionals & Loops
```python
# if-elif-else
if x > 0:
    print("positive")
elif x < 0:
    print("negative")
else:
    print("zero")

# for loops
for i in range(5):
    print(i)

for item in [1, 2, 3]:
    print(item)

for key, value in {"a": 1, "b": 2}.items():
    print(f"{key}: {value}")

# while loops
count = 0
while count < 5:
    print(count)
    count += 1

# List comprehensions
squares = [x**2 for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
```

### Functions
```python
def greet(name, greeting="Hello"):
    """Function with default parameter"""
    return f"{greeting}, {name}!"

def sum_all(*args):
    """Variable positional arguments"""
    return sum(args)

def create_profile(**kwargs):
    """Variable keyword arguments"""
    return kwargs

# Lambda functions
square = lambda x: x**2
sorted_names = sorted(["Alice", "bob", "Charlie"], key=lambda x: x.lower())

# Higher-order functions
def apply_operation(func, numbers):
    return [func(x) for x in numbers]
```

## 3. Object-Oriented Programming

### Classes and Inheritance
```python
class Animal:
    species_count = 0  # Class variable
    
    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age
        Animal.species_count += 1
    
    def speak(self):
        raise NotImplementedError("Subclass must implement")
    
    @property
    def is_adult(self):
        return self.age >= 3
    
    @classmethod
    def get_species_count(cls):
        return cls.species_count
    
    @staticmethod
    def animal_sound():
        return "Some generic animal sound"

class Dog(Animal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)
        self.breed = breed
    
    def speak(self):
        return f"{self.name} says Woof!"

# Multiple inheritance
class Flyable:
    def fly(self):
        return "Flying!"

class Bird(Animal, Flyable):
    def speak(self):
        return f"{self.name} says Tweet!"
```

### Magic Methods (Dunder Methods)
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"
    
    def __repr__(self):
        return f"Vector(x={self.x}, y={self.y})"
    
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __len__(self):
        return int((self.x**2 + self.y**0.5))
    
    def __getitem__(self, key):
        return [self.x, self.y][key]
    
    def __call__(self):
        return f"Vector magnitude: {len(self)}"

# Sample usage:
v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2              # Calls __add__
print(v3)                 # Calls __str__: Vector(4, 6)
print(repr(v3))           # Calls __repr__: Vector(x=4, y=6)
print(v1 == Vector(1, 2)) # Calls __eq__: True
print(len(v3))            # Calls __len__: 7
print(v3[0], v3[1])       # Calls __getitem__: 4 6
print(v3())               # Calls __call__: Vector magnitude: 7
```

### Encapsulation and Properties
```python
class BankAccount:
    def __init__(self, initial_balance=0):
        self._balance = initial_balance  # Protected
        self.__account_number = "12345"  # Private (name mangling)
    
    @property
    def balance(self):
        return self._balance
    
    @balance.setter
    def balance(self, value):
        if value < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = value
    
    def deposit(self, amount):
        self._balance += amount
```

## 4. Decorators

### Function Decorators
```python
import functools
import time

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f}s")
        return result
    return wrapper

def retry(max_attempts=3):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
                    print(f"Attempt {attempt + 1} failed: {e}")
            return wrapper
        return decorator

@timer
@retry(max_attempts=2)
def risky_operation():
    import random
    if random.random() < 0.5:
        raise Exception("Random failure")
    return "Success!"
```

### Class Decorators
```python
def singleton(cls):
    instances = {}
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance

@singleton
class Database:
    def __init__(self):
        self.connection = "Connected"
```

## 5. Iterators and Generators

### Iterators
```python
class NumberSequence:
    def __init__(self, start, end):
        self.start = start
        self.end = end
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.start >= self.end:
            raise StopIteration
        self.start += 1
        return self.start - 1

# Usage
for num in NumberSequence(1, 5):
    print(num)  # 1, 2, 3, 4
```

### Generators
```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

# Generator expression
squares = (x**2 for x in range(10))

# Real-world example: file processing
def read_large_file(file_path):
    with open(file_path, 'r') as file:
        for line in file:
            yield line.strip()
```

## 6. Exception Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Math error: {e}")
except Exception as e:
    print(f"General error: {e}")
else:
    print("No exceptions occurred")
finally:
    print("This always runs")

# Custom exceptions
class ValidationError(Exception):
    def __init__(self, message, code=None):
        super().__init__(message)
        self.code = code

def validate_age(age):
    if age < 0:
        raise ValidationError("Age cannot be negative", code="INVALID_AGE")
```

## 7. Context Managers

```python
# Built-in context manager
with open('file.txt', 'r') as f:
    content = f.read()

# Custom context manager (class-based)
class DatabaseConnection:
    def __enter__(self):
        print("Connecting to database")
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Closing database connection")
        if exc_type:
            print(f"Exception occurred: {exc_val}")
        return False  # Don't suppress exceptions

# Context manager using contextlib
from contextlib import contextmanager

@contextmanager
def timer_context():
    start = time.time()
    try:
        yield
    finally:
        end = time.time()
        print(f"Operation took {end - start:.2f}s")

# Usage
with timer_context():
    time.sleep(1)
```

## 8. Memory Management & Garbage Collection

### Reference Counting
```python
import sys

a = [1, 2, 3]
print(sys.getrefcount(a))  # Reference count

b = a  # Increases ref count
del b  # Decreases ref count
```

### Weak References
```python
import weakref

class Node:
    def __init__(self, value):
        self.value = value
        self.children = []
        self.parent = None

# Avoid circular references
node1 = Node(1)
node2 = Node(2)
node1.children.append(node2)
node2.parent = weakref.ref(node1)  # Weak reference to parent
```

## 9. Functional Programming

### Map, Filter, Reduce
```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Map
squared = list(map(lambda x: x**2, numbers))

# Filter
evens = list(filter(lambda x: x % 2 == 0, numbers))

# Reduce
sum_all = reduce(lambda x, y: x + y, numbers)

# Partial functions
from functools import partial

def multiply(x, y):
    return x * y

double = partial(multiply, 2)
print(double(5))  # 10
```

### Closures
```python
def outer_function(x):
    def inner_function(y):
        return x + y
    return inner_function

add_10 = outer_function(10)
print(add_10(5))  # 15

# Closure with mutable state
def counter():
    count = 0
    def increment():
        nonlocal count
        count += 1
        return count
    return increment

c = counter()
print(c())  # 1
print(c())  # 2
```

## 10. File Handling & I/O

```python
# Reading files
with open('data.txt', 'r') as f:
    content = f.read()           # Read entire file
    lines = f.readlines()        # Read all lines
    first_line = f.readline()    # Read one line

# Writing files
with open('output.txt', 'w') as f:
    f.write("Hello, World!\n")
    f.writelines(["Line 1\n", "Line 2\n"])

# JSON handling
import json

data = {"name": "Alice", "age": 30}
with open('data.json', 'w') as f:
    json.dump(data, f, indent=2)

with open('data.json', 'r') as f:
    loaded_data = json.load(f)

# CSV handling
import csv

with open('data.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerow(['Name', 'Age'])
    writer.writerow(['Alice', 30])
```

## 11. Modules and Packages

### Creating Modules
```python
# math_utils.py
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

PI = 3.14159

if __name__ == "__main__":
    print("Running math_utils directly")
```

### Importing
```python
import math_utils
from math_utils import add, PI
from math_utils import multiply as mult
import math_utils as mu

# Dynamic imports
import importlib
module = importlib.import_module('math_utils')
```

## 12. Regular Expressions

```python
import re

text = "Email: alice@example.com, Phone: 123-456-7890"

# Basic patterns
email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
phone_pattern = r'\d{3}-\d{3}-\d{4}'

# Finding matches
emails = re.findall(email_pattern, text)
phone_match = re.search(phone_pattern, text)

# Substitution
cleaned = re.sub(r'\d{3}-\d{3}-\d{4}', '[PHONE]', text)

# Compiled patterns (for performance)
email_regex = re.compile(email_pattern)
matches = email_regex.findall(text)
```

## 13. Threading & Multiprocessing

### Threading
```python
import threading
import time

def worker(name, delay):
    for i in range(3):
        print(f"Worker {name}: {i}")
        time.sleep(delay)

# Creating threads
t1 = threading.Thread(target=worker, args=("A", 1))
t2 = threading.Thread(target=worker, args=("B", 1.5))

t1.start()
t2.start()

t1.join()  # Wait for completion
t2.join()

# Thread synchronization
lock = threading.Lock()
shared_resource = 0

def increment():
    global shared_resource
    with lock:
        shared_resource += 1
```

### Multiprocessing
```python
import multiprocessing

def cpu_bound_task(n):
    return sum(i * i for i in range(n))

if __name__ == "__main__":
    with multiprocessing.Pool() as pool:
        results = pool.map(cpu_bound_task, [100000, 200000, 300000])
    print(results)
```

## 14. Error Handling & Debugging

### Exception Hierarchy
```python
# Built-in exceptions
try:
    value = int("not_a_number")
except ValueError as e:
    print(f"ValueError: {e}")
except Exception as e:
    print(f"General exception: {e}")

# Custom exceptions
class ValidationError(Exception):
    def __init__(self, message, field=None):
        super().__init__(message)
        self.field = field

def validate_email(email):
    if "@" not in email:
        raise ValidationError("Invalid email format", field="email")
```

### Debugging Techniques
```python
import logging
import pdb

# Logging
logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)

def debug_function(x):
    logger.debug(f"Input: {x}")
    result = x * 2
    logger.info(f"Result: {result}")
    return result

# Assertions
def divide(a, b):
    assert b != 0, "Division by zero"
    return a / b

# Debugger
def problematic_function():
    pdb.set_trace()  # Breakpoint
    return "debug me"
```

## 15. Data Structures Implementation

### Stack
```python
class Stack:
    def __init__(self):
        self.items = []
    
    def push(self, item):
        self.items.append(item)
    
    def pop(self):
        if self.is_empty():
            raise IndexError("Stack is empty")
        return self.items.pop()
    
    def peek(self):
        if self.is_empty():
            raise IndexError("Stack is empty")
        return self.items[-1]
    
    def is_empty(self):
        return len(self.items) == 0
```

### Queue
```python
from collections import deque

class Queue:
    def __init__(self):
        self.items = deque()
    
    def enqueue(self, item):
        self.items.append(item)
    
    def dequeue(self):
        if self.is_empty():
            raise IndexError("Queue is empty")
        return self.items.popleft()
    
    def is_empty(self):
        return len(self.items) == 0
```

### Linked List
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class LinkedList:
    def __init__(self):
        self.head = None
    
    def append(self, val):
        new_node = ListNode(val)
        if not self.head:
            self.head = new_node
            return
        
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node
    
    def prepend(self, val):
        new_node = ListNode(val)
        new_node.next = self.head
        self.head = new_node
    
    def delete(self, val):
        if not self.head:
            return
        
        if self.head.val == val:
            self.head = self.head.next
            return
        
        current = self.head
        while current.next and current.next.val != val:
            current = current.next
        
        if current.next:
            current.next = current.next.next
```

## 16. Algorithms (Common Interview Questions)

### Sorting
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quicksort(left) + middle + quicksort(right)

def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### Binary Search
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

def binary_search_recursive(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)
```

### Two Pointers Pattern
```python
def two_sum_sorted(arr, target):
    """Find two numbers that sum to target in sorted array"""
    left, right = 0, len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return []

def remove_duplicates(arr):
    """Remove duplicates from sorted array in-place"""
    if not arr:
        return 0
    
    write_index = 1
    for read_index in range(1, len(arr)):
        if arr[read_index] != arr[read_index - 1]:
            arr[write_index] = arr[read_index]
            write_index += 1
    
    return write_index
```

### Sliding Window
```python
def max_sum_subarray(arr, k):
    """Maximum sum of k consecutive elements"""
    if len(arr) < k:
        return None
    
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

def longest_substring_without_repeating(s):
    """Length of longest substring without repeating characters"""
    char_set = set()
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

## 17. Dynamic Programming

### Memoization
```python
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]
    
    if n <= 1:
        return n
    
    memo[n] = fibonacci_memo(n-1, memo) + fibonacci_memo(n-2, memo)
    return memo[n]

# Using functools.lru_cache
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci_cached(n):
    if n <= 1:
        return n
    return fibonacci_cached(n-1) + fibonacci_cached(n-2)
```

### Classic DP Problems
```python
def coin_change(coins, amount):
    """Minimum coins needed to make amount"""
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    
    for coin in coins:
        for i in range(coin, amount + 1):
            dp[i] = min(dp[i], dp[i - coin] + 1)
    
    return dp[amount] if dp[amount] != float('inf') else -1

def longest_common_subsequence(text1, text2):
    """Length of longest common subsequence"""
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]
```

## 18. Built-in Functions & Libraries

### Collections Module
```python
from collections import Counter, defaultdict, deque, namedtuple, OrderedDict

# Counter
text = "hello world"
char_count = Counter(text)
print(char_count.most_common(3))

# defaultdict
dd = defaultdict(list)
dd['key'].append('value')  # No KeyError

# deque (double-ended queue)
dq = deque([1, 2, 3])
dq.appendleft(0)
dq.pop()

# namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
print(p.x, p.y)
```

### Itertools
```python
import itertools

# Combinations and permutations
data = [1, 2, 3]
print(list(itertools.combinations(data, 2)))  # [(1, 2), (1, 3), (2, 3)]
print(list(itertools.permutations(data, 2)))  # [(1, 2), (1, 3), (2, 1), ...]

# Infinite iterators
counter = itertools.count(start=5, step=2)  # 5, 7, 9, 11, ...
repeater = itertools.repeat('hello', 3)     # 'hello', 'hello', 'hello'

# Grouping
data = [('a', 1), ('a', 2), ('b', 3), ('b', 4)]
grouped = itertools.groupby(data, key=lambda x: x[0])
for key, group in grouped:
    print(f"{key}: {list(group)}")
```

## 19. Common Gotchas & Best Practices

### Mutable Default Arguments
```python
# Wrong
def append_to_list(item, target_list=[]):
    target_list.append(item)
    return target_list

# Right
def append_to_list(item, target_list=None):
    if target_list is None:
        target_list = []
    target_list.append(item)
    return target_list
```

### Late Binding Closures
```python
# Wrong
functions = []
for i in range(3):
    functions.append(lambda: i)  # All return 2

# Right
functions = []
for i in range(3):
    functions.append(lambda x=i: x)  # Capture current value
```

### Shallow vs Deep Copy
```python
import copy

original = [[1, 2], [3, 4]]
shallow = copy.copy(original)
deep = copy.deepcopy(original)

original[0][0] = 999
print(shallow)  # [[999, 2], [3, 4]] - affected
print(deep)     # [[1, 2], [3, 4]] - not affected
```

## 20. Testing

### Unit Testing
```python
import unittest

class Calculator:
    def add(self, a, b):
        return a + b
    
    def divide(self, a, b):
        if b == 0:
            raise ValueError("Cannot divide by zero")
        return a / b

class TestCalculator(unittest.TestCase):
    def setUp(self):
        self.calc = Calculator()
    
    def test_add(self):
        self.assertEqual(self.calc.add(2, 3), 5)
    
    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            self.calc.divide(10, 0)

if __name__ == "__main__":
    unittest.main()
```

### Pytest (More Popular)
```python
import pytest

def test_add():
    calc = Calculator()
    assert calc.add(2, 3) == 5

def test_divide_by_zero():
    calc = Calculator()
    with pytest.raises(ValueError):
        calc.divide(10, 0)

# Fixtures
@pytest.fixture
def calculator():
    return Calculator()

def test_with_fixture(calculator):
    assert calculator.add(1, 1) == 2
```

## 21. Performance & Optimization

### Timing Code
```python
import timeit

# Simple timing
def slow_function():
    return sum(range(1000))

execution_time = timeit.timeit(slow_function, number=1000)
print(f"Average time: {execution_time/1000:.6f}s")

# Profile with cProfile
import cProfile
cProfile.run('slow_function()')
```

### Memory Usage
```python
import sys
from memory_profiler import profile

@profile
def memory_intensive():
    big_list = [i for i in range(1000000)]
    return sum(big_list)

# Check object size
data = [1, 2, 3, 4, 5]
print(f"Size: {sys.getsizeof(data)} bytes")
```

## 22. Common Interview Questions & Patterns

### String Manipulation
```python
def is_palindrome(s):
    """Check if string is palindrome (ignore case, spaces, punctuation)"""
    cleaned = ''.join(char.lower() for char in s if char.isalnum())
    return cleaned == cleaned[::-1]

def reverse_words(s):
    """Reverse words in a string"""
    return ' '.join(s.split()[::-1])

def first_non_repeating_char(s):
    """Find first non-repeating character"""
    char_count = {}
    for char in s:
        char_count[char] = char_count.get(char, 0) + 1
    
    for char in s:
        if char_count[char] == 1:
            return char
    return None
```

### Array Problems
```python
def find_missing_number(nums):
    """Find missing number in range [0, n]"""
    n = len(nums)
    expected_sum = n * (n + 1) // 2
    actual_sum = sum(nums)
    return expected_sum - actual_sum

def rotate_array(nums, k):
    """Rotate array to the right by k steps"""
    k = k % len(nums)
    nums[:] = nums[-k:] + nums[:-k]

def merge_intervals(intervals):
    """Merge overlapping intervals"""
    if not intervals:
        return []
    
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    
    for current in intervals[1:]:
        last = merged[-1]
        if current[0] <= last[1]:
            merged[-1] = [last[0], max(last[1], current[1])]
        else:
            merged.append(current)
    
    return merged
```

## 23. Metaclasses

- A metaclass is a "class of a class": it defines how classes behave. By default, Python uses `type` as the metaclass.
- Custom metaclasses are created by subclassing `type` and overriding methods like `__new__` or `__init__`.
- Use cases: automatically register subclasses, enforce class attributes/methods, modify class creation.
- Specify a metaclass with `class Foo(metaclass=Meta): ...`
- Prefer class decorators for most use cases; use metaclasses only for advanced class customization.

```python
# Example: Enforcing all classes have a 'speak' method
class RequireSpeak(type):
    def __init__(cls, name, bases, dct):
        if 'speak' not in dct:
            raise TypeError("Class must define 'speak' method")
        super().__init__(name, bases, dct)

class Animal(metaclass=RequireSpeak):
    def speak(self):
        return "Sound"

a = Animal()
print(a.speak())  # Output: Sound
```

## 24. Descriptors

- A descriptor is any object that defines at least one of `__get__`, `__set__`, or `__delete__` methods and is used as a class attribute.
- **Data descriptor**: defines both `__get__` and `__set__` (e.g., property with setter); **non-data descriptor**: only `__get__`.
- The `property` built-in is implemented using descriptors; allows custom logic for attribute access.
- Use descriptors for validation, computed properties, or managing access to attributes.

```python
# Example: Descriptor for positive values
class Positive:
    def __get__(self, instance, owner):
        return instance._value
    def __set__(self, instance, value):
        if value < 0:
            raise ValueError("Value must be positive")
        instance._value = value

class Account:
    balance = Positive()
    def __init__(self, balance):
        self.balance = balance

a = Account(100)
a.balance = 50
# a.balance = -10  # Raises ValueError
```

## 25. Advanced String Operations

- Know all string formatting styles: f-strings (`f"{x}"`), `.format()`, and `%` formatting; prefer f-strings for new code.
- Understand the difference between Unicode strings (`str`) and byte strings (`bytes`); know how to encode/decode.
- String interning: Python may reuse immutable string objects for efficiency; use `sys.intern()` for large sets of repeated strings.
- Strings are immutable; all string operations create new objects.

```python
# Example: String formatting and interning
name = "Alice"
print(f"Hello, {name}!")  # f-string
print("Hello, {}!".format(name))  # .format()
print("Hello, %s!" % name)  # % formatting

import sys
a = sys.intern("hello")
b = sys.intern("hello")
print(a is b)  # True
```

## 26. Python Internals

- The GIL (Global Interpreter Lock) allows only one thread to execute Python bytecode at a time; affects multi-threaded CPU-bound code.
- Python source code is compiled to bytecode (`.pyc` files), which is then interpreted by the CPython VM.
- Use the `dis` module to inspect Python bytecode: `import dis; dis.dis(func)`.
- Know how the GIL impacts concurrency and when to use multiprocessing instead of threading.

```python
# Example: Inspecting bytecode
def add(x, y):
    return x + y

import dis
dis.dis(add)
```

## 27. Design Patterns

- **Singleton**: ensure only one instance of a class exists (use a class variable or decorator).
- **Factory**: a function or class that creates objects, often based on input parameters.
- **Observer**: objects subscribe to events and get notified on changes (use callbacks or signals).
- Pythonic alternatives: use modules as singletons, or leverage first-class functions for factories.
- Be able to recognize and implement these patterns in Python.

```python
# Example: Singleton pattern
class Singleton:
    _instance = None
    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super().__new__(cls)
        return cls._instance

s1 = Singleton()
s2 = Singleton()
print(s1 is s2)  # True
```

## 28. Database Integration

- Connect to SQLite with `sqlite3` or to PostgreSQL/MySQL with libraries like `psycopg2` or `mysql-connector-python`.
- ORM basics: define models as classes, use sessions to query and persist data (SQLAlchemy).
- Always use context managers (`with` statement) for database connections to ensure cleanup.
- Prevent SQL injection by using parameterized queries, never string formatting for SQL.

```python
# Example: SQLite connection and query
import sqlite3
with sqlite3.connect(":memory:") as conn:
    c = conn.cursor()
    c.execute("CREATE TABLE users (id INTEGER, name TEXT)")
    c.execute("INSERT INTO users VALUES (?, ?)", (1, "Alice"))
    c.execute("SELECT * FROM users")
    print(c.fetchall())  # [(1, 'Alice')]
```

## 29. Web Frameworks Basics

- Flask: minimal web framework; Django: full-featured framework. Know how to define routes and handle requests.
- Understand the HTTP request/response cycle: request comes in, routed to a view, response returned.
- REST API: stateless endpoints using HTTP verbs (GET, POST, PUT, DELETE).
- Know where to add authentication (middleware/decorators) and input validation.

```python
# Example: Flask route
from flask import Flask
app = Flask(__name__)

@app.route("/hello")
def hello():
    return "Hello, World!"

# Run with: flask run
```

## 30. Data Science Libraries

- NumPy: create arrays, perform vectorized operations, understand broadcasting rules.
- Pandas: create DataFrames, select/filter data, use `groupby`, handle missing data.
- Import/export data: `read_csv`, `to_csv`, `read_excel`, `read_json`.
- Practice common data manipulation: filtering, aggregation, reshaping.

```python
# Example: NumPy and Pandas basics
import numpy as np
import pandas as pd

arr = np.array([1, 2, 3])
print(arr * 2)  # [2 4 6]

df = pd.DataFrame({"A": [1, 2], "B": [3, 4]})
print(df["A"].mean())  # 1.5
```

## 31. Networking & APIs

- Use the `requests` library to make HTTP requests: `requests.get()`, `requests.post()`, handle headers and JSON.
- Parse JSON with `response.json()` and serialize with `json.dumps()`.
- Basic socket programming: create TCP/UDP clients and servers with the `socket` module.
- Always handle exceptions and timeouts in network code.

```python
# Example: HTTP GET request
import requests
response = requests.get("https://api.github.com")
print(response.status_code)
print(response.json())
```

## 32. Security Considerations

- Always validate and sanitize user input to prevent injection attacks.
- Avoid using `eval` and `pickle` on untrusted data; prefer `json` for serialization.
- Use context managers for file/database operations to avoid resource leaks.
- Be aware of common vulnerabilities: code injection, insecure deserialization, improper permissions.

```python
# Example: Safe JSON deserialization
import json
data = '{"name": "Alice"}'
obj = json.loads(data)
print(obj["name"])
```

## 33. Python 3 Features

- Type hints: annotate function arguments and return types; use `mypy` for static checking.
- Use `pathlib.Path` for filesystem paths instead of `os.path`.
- Prefer f-strings for formatting; know about new syntax features (e.g., assignment expressions `:=`).
- Pattern matching (`match` statement, Python 3.10+): use for matching on structure, not just values.

```python
# Example: Type hints and pattern matching
from pathlib import Path

def greet(name: str) -> str:
    return f"Hello, {name}"

p = Path("file.txt")
print(p.exists())

# Pattern matching (Python 3.10+)
def http_status(status):
    match status:
        case 200:
            return "OK"
        case 404:
            return "Not Found"
        case _:
            return "Unknown"
print(http_status(404))  # Not Found
```
