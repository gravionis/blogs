+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = 'System Design Interview Concepts'
tags = ['Event Driven Architecture', 'Microservices', 'Interview']
+++

System design is a critical aspect of software engineering that involves creating scalable, reliable, and efficient systems. This document explores key concepts and strategies required for designing robust systems, including networking, databases, scalability, caching, and modern architectural patterns. It serves as a comprehensive guide for understanding the foundational and advanced principles of system design.

# Table of Contents

- [Approach](#approach)
- [HTTPS Certificates in System Design](#https-certificates-in-system-design)
- [Networking and Communication](#networking-and-communication)
  - [Client Server Architecture](#client-server-architecture)
  - [IP Address](#ip-address)
  - [DNS](#dns)
  - [Proxy/Reverse Proxy](#proxyreverse-proxy)
  - [Latency](#latency)
  - [HTTP/HTTPS and MASL (Mutual Authentication Security Layers)](#httphttps-and-masl-mutual-authentication-security-layers)
  - [WebSockets](#websockets)
  - [Webhooks](#webhooks)
- [APIs and Integration](#apis-and-integration)
  - [APIs](#apis)
  - [REST API](#rest-api)
  - [GraphQL](#graphql)
  - [API Gateway](#api-gateway)
  - [Idempotency](#idempotency)
  - [REST and REST Maturity Model](#rest-and-rest-maturity-model)
- [Databases and Storage](#databases-and-storage)
  - [Databases](#databases)
  - [SQL vs NoSQL vs Object Store](#sql-vs-nosql-vs-object-store)
  - [Database Indexing](#database-indexing)
  - [Replication](#replication)
  - [Sharding](#sharding)
  - [Vertical Partitioning](#vertical-partitioning)
  - [Caching](#caching)
  - [ACID vs BASE](#acid-vs-base)
  - [Normalization vs Denormalization](#normalization-vs-denormalization)
  - [CAP Theorem](#cap-theorem)
  - [Consistency Models: Linearizability vs Causal Consistency](#consistency-models-linearizability-vs-causal-consistency)
  - [Blob Storage](#blob-storage)
- [Scalability and Performance](#scalability-and-performance)
  - [Vertical and Horizontal Scaling](#vertical-and-horizontal-scaling)
  - [Algorithmic Scaling](#algorithmic-scaling)
  - [Load Balancers](#load-balancers)
  - [Rate Limiting](#rate-limiting)
  - [Content Delivery Optimization](#content-delivery-optimization)
  - [Zero Downtime Deployment](#zero-downtime-deployment)
- [Common Design Patterns and Architecture](#common-design-patterns-and-architecture)
  - [Event-Driven Architecture](#event-driven-architecture)
  - [Data Partitioning Strategies](#data-partitioning-strategies)
  - [Eventual Consistency](#eventual-consistency)
  - [Leader Election](#leader-election)
  - [Circuit Breaker Pattern](#circuit-breaker-pattern)
  - [Throttling and Backpressure](#throttling-and-backpressure)
  - [Service Discovery](#service-discovery)
  - [Microservices](#microservices)
  - [Message Queues](#message-queues)
- [Monitoring, Resiliency, and Security](#monitoring-resiliency-and-security)
  - [Monitoring and Observability](#monitoring-and-observability)
  - [Data Compression](#data-compression)
  - [Authentication and Authorization](#authentication-and-authorization)
  - [Data Backup and Recovery](#data-backup-and-recovery)
  - [Chaos Engineering](#chaos-engineering)
- [Development and Deployment](#development-and-deployment)
  - [Concurrency Control](#concurrency-control)
  - [Immutable Infrastructure](#immutable-infrastructure)
  - [Blue-Green Deployment](#blue-green-deployment)
- [Theoretical Concepts](#theoretical-concepts)
  - [Search Systems](#search-systems)
- [Data Processing](#data-processing)
  - [Data Streaming](#data-streaming)
- [Miscellaneous](#miscellaneous)
  - [Rate Shaping](#rate-shaping)

## Approach
- Do not directly start designing; every problem is unique. Think of every problem as designing and building a bridge. You must understand:
  - **Whom or What you are building for**  
    - target users or audience and their count.  
    - Expected traffic or load  
    - User behavior e.g. Celebrity Problem 
    - Interaction patterns.  
    - Account for user demographics and geographic distribution.  
    - Evaluate the specific needs or goals of the users.
  - **Where you are building** (the environment or constraints).
  - **How you build**.

## Steps:
- **Understand your use case**: Clearly define the problem and its requirements.
- **Ask the right questions**: Gather Necessary details, NO assumptions.
- **Decide the modules**: Break the big problem into smaller, manageable parts (e.g., defining context boundaries). Ask which they want you to tackle first.
- **Design with key considerations**:  Address other critical "ilities"
     - **Availability**
     - **Reliability**
     - **Maintainability**
     - **Performance**
     - **Scalability**
     - **Cost-efficiency**
     - **Security**
     - **Flexibility**
     (Always remind yourself - everything fails)
---
## HTTPS Certificates in System Design

In system design, **HTTPS certificates** are essential for securing communication between clients (e.g., web browsers, mobile apps) and servers. They are used to encrypt data, verify server identity, and ensure secure communication channels in modern web and microservice architectures.

---

## Key Points about HTTPS Certificates

### 1. **What is an HTTPS Certificate?**
- **HTTPS certificates** are **X.509 certificates** used in **TLS (Transport Layer Security)** for encrypting and securing HTTP traffic.
- They contain the **public key** of a server, and are signed by a trusted **Certificate Authority (CA)** to confirm the authenticity of the server.

### 2. **Role in HTTPS Communication:**
- **Encryption**: HTTPS certificates use **TLS** to encrypt data in transit, ensuring that information exchanged between client and server is private and secure.
- **Authentication**: The certificate proves the server's identity, assuring clients that they are communicating with the correct, trusted server.
- **Data Integrity**: It ensures that data cannot be tampered with while in transit.

---

## HTTPS Flow in System Design

1. **DNS Resolution** → The domain name (e.g., `example.com`) is resolved to an IP address.
2. **TCP Handshake** → A 3-way handshake is established between the client and server.
3. **TLS Handshake**:
   - The client requests a secure connection and receives the server's certificate.
   - The client verifies the certificate's authenticity (checking the CA and validity period).
   - The client and server exchange keys to encrypt further communication.
4. **Secure Communication**: The HTTP request and response occur over the encrypted TLS channel.
5. **Connection Termination**: Once communication is complete, the connection is securely closed.

---

## HTTPS Certificate Components

1. **Public Key**: Used for encryption and establishing a secure connection.
2. **Issuer**: The Certificate Authority (CA) that issued the certificate.
3. **Subject**: The entity (e.g., website, server) being identified by the certificate.
4. **Validity Period**: The certificate’s expiration date.
5. **Signature**: A digital signature from the CA, ensuring the certificate's authenticity.
6. **Extensions**: Additional metadata, such as **Subject Alternative Names (SANs)**, which allow a single certificate to cover multiple domains.

---

## Use Cases in System Design

### 1. **Web Applications**
- HTTPS certificates are used to secure user data, such as login credentials and payment details, during transmission between the browser and server.
- **SSL/TLS** ensures that users can trust the site and prevents **man-in-the-middle attacks**.

### 2. **API Security**
- APIs use HTTPS certificates to secure communication between clients and services, ensuring that data transmitted between services is encrypted and authenticated.
- **API Gateways** often enforce HTTPS for all incoming and outgoing traffic to secure internal and external communications.

### 3. **Microservices Communication**
- In microservices architectures, services communicate securely using **TLS** certificates.
- Certificates can be used with **mTLS (Mutual TLS)**, where both the client and the server authenticate each other.
- This is common for ensuring trust between services within a **private network**.

### 4. **Certificate Pinning**
- To prevent attacks, some systems implement **certificate pinning** to ensure that only a specific, trusted certificate can be used, even if it’s issued by a trusted CA.

---

## Design Considerations for HTTPS Certificates

### 1. **Certificate Management:**
   - **Renewal**: Certificates must be renewed periodically (typically every 1-2 years).
   - **Revocation**: Certificates must be revoked if compromised, and Certificate Revocation Lists (CRLs) or **OCSP (Online Certificate Status Protocol)** can be used to check the certificate status.

### 2. **Load Balancers and API Gateways:**
   - **SSL Termination**: In many architectures, HTTPS connections are terminated at a **load balancer** or **API Gateway**. This means the secure connection between the client and the gateway is decrypted, and the communication between services may continue over plain HTTP or encrypted further.

### 3. **Security Best Practices:**
   - Use strong encryption algorithms (e.g., **TLS 1.2 or 1.3**).
   - **Perfect Forward Secrecy (PFS)** should be enabled to ensure that past sessions are not compromised even if the server's private key is leaked.
   - Regularly update certificates and private keys.
   - Store private keys securely and limit access.

---

## Key Takeaways for System Design

- **HTTPS certificates** are crucial for securing **web traffic** and **API communications** in modern system architectures.
- They ensure **confidentiality**, **integrity**, and **authentication** between clients and servers.
- Proper **certificate management** (renewal, revocation, etc.) is key for maintaining security.
- **SSL/TLS termination** at **API Gateways** or **load balancers** can simplify management but must be carefully designed to ensure traffic is encrypted when needed.
- **mTLS** can be used for mutual authentication between services, adding an additional layer of security in microservices architectures.


## Networking and Communication
### Client Server Architecture
### IP Address
### DNS
### Proxy/Reverse Proxy
### Latency
### HTTP/HTTPS and MASL (Mutual Authentication Security Layers)

## 🔹 1. HTTP / HTTPS in System Design

### 📌 HTTP
- Stateless protocol for transferring hypertext and media between client and server.
- Operates over **TCP** (usually port **80**).
- Requests consist of **methods** (GET, POST, PUT, DELETE), **headers**, and optionally a **body**.
- No built-in encryption → data sent in plaintext.

### 📌 HTTPS
- HTTP over **TLS (Transport Layer Security)** → operates on port **443**.

**Provides:**
- 🔒 **Confidentiality:** Encrypts data.
- 🛡️ **Integrity:** Detects tampering.
- 🧾 **Authentication:** Validates server identity via SSL/TLS certificates.

**Used In:**
- Web apps  
- REST APIs  
- Microservices communication  
- IoT and mobile devices  

## 🔹 Details of handshake 
<img width="3000" height="3336" alt="image" src="https://github.com/user-attachments/assets/2e8bf550-4932-4c84-a2ca-b3034b57c1f8" />

### 1. Client Hello
The client initiates the handshake by sending:
- A list of supported **cipher suites** (algorithms for encryption, key exchange, etc.).
- A **`client_random`** value — a 32-byte random number.

#### 🔎 Why `client_random`?
- Adds **entropy** to the key derivation process.
- Ensures each session is **unique**, even if the same algorithms are used.
- Helps prevent **replay attacks** by making the handshake unpredictable.

### 2. Server Hello + Certificate
The server responds with:
- A selected **cipher suite** from the client's list.
- Its own **`server_random`** value.
- A **digital certificate** (usually X.509) containing its public key and identity.

#### 🔎 Why the Certificate?
- Allows the client to **authenticate** the server.
- The client checks:
  - Is the certificate signed by a trusted Certificate Authority (CA)?
  - Is it still valid (not expired)?
  - Does the domain match?

### 3. Key Exchange and Session Key Derivation
Depending on the chosen cipher suite (e.g., ECDHE), the client and server:
- Exchange **ephemeral public keys**.
- Each side uses its private key and the other’s public key to compute a **shared secret**.
- They use a **Key Derivation Function (KDF)** to combine:
  - The shared secret
  - `client_random`
  - `server_random`
  → to derive **symmetric session keys**.
#### 🔐 How the Shared Secret Is Computed in ECDHE

🔄 Key Generation
**Client generates:**

- Private key: a
- Public key: A = aG
**Server generates:**

- Private key: b
- Public key: B = bG
Here, G is a known base point on the elliptic curve.
- **Client computes**:  
  `S = a * B = a * (bG) = abG`
- **Server computes**:  
  `S = b * A = b * (aG) = abG`
✅ Both arrive at the **same shared secret** `S = abG`.

#### 🔎 Why Ephemeral Keys (ECDHE)?
- Provides **forward secrecy**: even if long-term keys are compromised, past sessions remain secure.
- Ensures that each session has **unique encryption keys**.

### 4. Finished Messages
- Both sides send encrypted "Finished" messages to confirm that the handshake was successful.
- From this point on, all communication is encrypted using the derived session keys.

---

### 🔐 Summary of Key Components

| Component        | Purpose                                      |
|------------------|----------------------------------------------|
| `client_random`  | Adds entropy, uniqueness, and prevents replay attacks |
| `server_random`  | Same as above, from the server side          |
| Certificate      | Authenticates the server (and optionally the client) |
| Ephemeral Keys   | Used to compute a shared secret securely     |
| Session Keys     | Encrypt and authenticate all further communication |


---

## 🔐 What is Mutual Authentication (mTLS)?

### 📌 Common Use Cases

| Use Case                      | Why Use mTLS?                                     |
|------------------------------|---------------------------------------------------|
| Service-to-service (microservices) | Ensure only trusted services communicate          |
| APIs for fintech / healthcare | Regulatory compliance (HIPAA, PCI-DSS)            |
| IoT Devices ↔ Cloud          | Authenticate individual devices securely          |
| Enterprise internal apps     | Add trust within a private/internal network       |

## 🔹 Details of handshake 
<img width="1452" height="2322" alt="image" src="https://github.com/user-attachments/assets/93556c5e-3e0b-42a2-90e0-aae7c0ad1da6" />

### 1. Client Hello
- Client sends supported cipher suites and `client_random`.

### 2. Server Hello + Certificate
- Server responds with:
  - Chosen cipher suite
  - `server_random`
  - Server certificate

### 3. Server Requests Client Certificate
- Server sends a `CertificateRequest` message.

### 4. Client Sends Certificate
- Client sends its certificate for authentication.

### 5. Key Exchange
- Both sides exchange ephemeral public keys (e.g., via ECDHE).
- Each side computes the shared secret using its private key and the other’s public key.

### 6. Certificate Verification
- Server verifies the client’s certificate.
- Client verifies the server’s certificate.

### 7. Finished Messages
- Both sides send encrypted "Finished" messages.
- Secure communication begins using derived session keys.



### WebSockets
---
### Webhooks
---
## APIs and Integration
### APIs
---
### REST API
---
### GraphQL
---
### API Gateway
---
### Idempotency
---
## REST and REST Maturity Model
### What is REST?
REST (Representational State Transfer) is an architectural style for designing networked applications. It relies on stateless communication and standard HTTP methods to enable interaction between clients and servers. RESTful APIs are widely used for their simplicity, scalability, and compatibility with web standards.

Key principles of REST include:
- **Statelessness**: Each request from a client to a server must contain all the information needed to understand and process the request.
- **Client-Server Architecture**: Separation of concerns between the client and server, allowing them to evolve independently.
- **Uniform Interface**: A consistent and standardized way of interacting with resources.
- **Resource-Based**: Resources are identified using URIs (Uniform Resource Identifiers).
- **Cacheability**: Responses must define whether they are cacheable to improve performance.
- **Layered System**: The architecture can have multiple layers, such as load balancers and proxies, to improve scalability and security.

### REST Maturity Model
The REST Maturity Model, introduced by Leonard Richardson, defines levels of maturity for RESTful APIs. It helps evaluate how closely an API adheres to REST principles.

![](../REST.png)

#### Level 0: The Swamp of POX
- APIs at this level use a single URI and rely on HTTP POST for all interactions.
- They often resemble RPC (Remote Procedure Call) or SOAP (Simple Object Access Protocol).

#### Level 1: Resources
- Introduces the concept of resources, each identified by a unique URI.
- HTTP methods are not yet fully utilized.

#### Level 2: HTTP Verbs
- Uses standard HTTP methods (GET, POST, PUT, DELETE, etc.) to perform operations on resources.
- Improves clarity and aligns with REST principles.

#### Level 3: Hypermedia Controls (HATEOAS)
- Hypermedia as the Engine of Application State (HATEOAS) is implemented.
- Clients can navigate the API dynamically using links provided in responses.
- This level achieves full REST maturity by enabling discoverability and self-documentation.

### Benefits of REST Maturity
- **Scalability**: Higher levels of maturity improve scalability by leveraging HTTP standards.
- **Interoperability**: Adherence to REST principles ensures compatibility across different platforms.
- **Maintainability**: A well-designed RESTful API is easier to maintain and extend.
- **Discoverability**: HATEOAS enables clients to discover available actions dynamically.

By understanding and applying the REST Maturity Model, developers can design APIs that are robust, scalable, and aligned with modern web standards.

---
## Databases and Storage
### Databases
---
### SQL vs NoSQL vs Object Store

When designing a system, choosing the right data storage solution is crucial. The three main categories are **SQL databases**, **NoSQL databases**, and **Object Stores**. Each serves different use cases and has unique characteristics.

#### SQL Databases (Relational Databases)

- **Examples:** MySQL, PostgreSQL, Oracle, Microsoft SQL Server
- **Data Model:** Structured, tabular data with predefined schemas (tables, rows, columns)
- **Query Language:** SQL (Structured Query Language)
- **Transactions:** Strong ACID guarantees (Atomicity, Consistency, Isolation, Durability)
- **Use Cases:** Applications requiring complex queries, joins, and strong consistency (e.g., banking, ERP, CRM)
- **Strengths:** Data integrity, complex querying, relationships, mature ecosystem
- **Limitations:** Vertical scaling, rigid schema, less suited for unstructured or rapidly evolving data

#### NoSQL Databases

- **Examples:** MongoDB (Document), Cassandra (Wide-column), Redis (Key-Value), Neo4j (Graph)
- **Data Model:** Flexible, can be document, key-value, column-family, or graph-based
- **Schema:** Schema-less or dynamic schemas; can handle semi-structured or unstructured data
- **Transactions:** Typically BASE properties (Basically Available, Soft state, Eventually consistent)
- **Use Cases:** High scalability, large volumes of diverse data, real-time analytics, IoT, social networks
- **Strengths:** Horizontal scaling, flexible data models, high write/read throughput
- **Limitations:** Weaker consistency (eventual consistency), limited support for complex joins, less mature tooling

#### Object Store

- **Examples:** Amazon S3, Google Cloud Storage, Azure Blob Storage, MinIO
- **Data Model:** Stores data as objects (blobs) with metadata and a unique identifier; no schema or tables
- **Access:** Accessed via APIs (REST, SDKs); not a database—optimized for storing and retrieving large files
- **Transactions:** No ACID/BASE guarantees; eventual consistency for some operations
- **Use Cases:** Storing unstructured data (images, videos, backups, logs, large files), data lakes, static website hosting
- **Strengths:** Virtually unlimited scalability, low cost for large data, durability, global access
- **Limitations:** Not suitable for transactional data or complex queries; eventual consistency; slower for small, frequent reads/writes

#### Comparison Table

| Feature         | SQL (Relational)         | NoSQL                    | Object Store                |
|-----------------|-------------------------|--------------------------|-----------------------------|
| **Data Model**  | Tables (rows/columns)   | Flexible (JSON, KV, etc) | Objects (blobs + metadata)  |
| **Schema**      | Fixed                   | Dynamic/Schema-less      | None                        |
| **Query**       | SQL                     | Varies (NoSQL APIs)      | API (REST/S3)               |
| **Transactions**| ACID                    | BASE (usually)           | None                        |
| **Scaling**     | Vertical (mostly)       | Horizontal               | Horizontal                  |
| **Best For**    | Structured, relational  | Semi/unstructured, scale | Unstructured, large files   |
| **Examples**    | MySQL, PostgreSQL       | MongoDB, Cassandra       | S3, GCS, Azure Blob         |

**Summary:**  
- Use **SQL** for structured data and strong consistency.
- Use **NoSQL** for flexible, scalable, high-throughput needs.
- Use **Object Store** for unstructured, large-scale file storage—not as a database.

---
### Database Indexing
---
### Replication
---
### Sharding
---
### Vertical Partitioning
---
### Caching

Caching is the process of storing frequently accessed data in a temporary storage layer to improve system performance and reduce latency. 

#### Advantages of Caching

1. **Improved Performance**: Reduces response time by serving data from faster storage layers (e.g., memory).  

2. **Reduced Latency**: Minimizes delays in data retrieval, enhancing user experience.  

3. **Lower Database Load**: Decreases the number of direct queries to the database, reducing resource usage.  

4. **Scalability**: Helps handle increased traffic by offloading requests from the primary data source.  

5. **Cost Efficiency**: Reduces operational costs by optimizing resource utilization.  

#### Disadvantages of Caching

1. **Data Staleness**: Cached data may become outdated if not properly invalidated or refreshed.  

2. **Complexity**: Implementing and managing caching layers adds complexity to the system.  

3. **Cache Misses**: If data is not found in the cache, it can lead to slower performance as the system falls back to the original data source.  

4. **Memory Overhead**: Caching requires additional memory, which can increase infrastructure costs.  

5. **Consistency Challenges**: Ensuring data consistency between the cache and the source of truth can be difficult.  

#### Strategies

1. **Cache-Aside**: The application checks the cache first. If the data is not found, it fetches from the database and updates the cache. Commonly used for read-heavy workloads.  

2. **Write-Through**: Data is written to the cache and the database simultaneously. Ensures data consistency but may introduce higher write latency.  

3. **Write-Behind**: Data is written to the cache first and asynchronously updated in the database. Improves write performance but risks data loss during failures.  

4. **Read-Through**: The application interacts only with the cache. If the data is not in the cache, the cache fetches it from the database. Simplifies application logic but adds complexity to the caching layer.  

#### Measuring Cache Effectiveness

1. **Calculate the Cache Hit Rate**: Measure the percentage of requests served from the cache versus the total requests. A high hit rate indicates effective caching.  

2. **Analyze Cache Eviction Rate**: Monitor how often data is evicted from the cache due to capacity limits. Optimize cache size and eviction policies to reduce unnecessary evictions.  

3. **Monitor Data Consistency**: Ensure that cached data remains consistent with the source of truth (e.g., database). Use appropriate invalidation and expiration mechanisms.  

4. **Determine the Right Cache Expiration Time**: Set expiration times based on data usage patterns and freshness requirements. Avoid stale data while minimizing unnecessary cache misses.

#### Example Use Cases for Caching

1. **URL Shortener**: Cache `ShortCode → URL` mappings. Strategy: LRU for frequently accessed URLs.

2. **User Profile Service**: Cache user profiles with TTL for frequent reads. Challenge: Cache invalidation and consistency.

3. **Weather Forecast API**: Cache responses based on `city+date`. Set TTL based on forecast freshness.

4. **Rate Limiter Service**: Cache token bucket or sliding window counters per user. Use Redis or in-memory store with expiration.

5. **Product Catalog**: Cache product details at edge/CDN. Strategy: Write-through or refresh-on-write.

6. **Twitter Feed**: Cache user timelines and precompute recent tweets. Eviction policy: LRU or LFU.

7. **Geolocation Service**: Cache frequently accessed IP ranges. Use TTL for DNS/IP lookups.

8. **Session Management**: Store sessions in Redis with TTL. Trade-off: In-memory vs database storage.

9. **Distributed Cache System**: Handle replication vs partitioning. Prevent hot keys and cache stampede.

10. **Online Code Editor**: Cache user preferences and recent submissions. Use client-side and server-side caching.

#### References

- [Cache Strategies - Medium](https://medium.com/@mmoshikoo/cache-strategies-996e91c80303)

---
### ACID vs BASE

#### ACID Properties
ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties are essential for traditional relational databases to ensure reliable transactions:
- **Atomicity**: Ensures that a transaction is all-or-nothing. If one part fails, the entire transaction is rolled back.
- **Consistency**: Guarantees that a transaction brings the database from one valid state to another, maintaining all defined rules.Always preserve the data integrity.
- **Isolation**: Ensures that concurrent transactions do not interfere with each other. Don't step on each other shoes. The various problems

  | Isolation Level      | Dirty Reads | Non-Repeatable Reads | Phantom Reads | Description |
  |----------------------|-------------|-----------------------|----------------|-------------|
  | **Read Uncommitted** | ✅ Allowed  | ✅ Allowed            | ✅ Allowed     | Minimal isolation, allows all anomalies. |
  | **Read Committed**   | ❌ Prevented| ✅ Allowed            | ✅ Allowed     | Only committed data is visible. Default in many databases. |
  | **Repeatable Read**  | ❌ Prevented| ❌ Prevented          | ✅ Allowed     | Rows cannot change, but new rows may appear (phantoms). |
  | **Serializable**     | ❌ Prevented| ❌ Prevented          | ❌ Prevented   | Full isolation, transactions execute as if sequentially. |

  - **Dirty Read**: Transaction reads data written by another uncommitted transaction.Example: T1 reads a value updated by T2, but T2 hasn't committed. **Solution**: Use `Read Committed` or higher.
  
  - **Non-Repeatable Read**: A row is read twice and returns different data due to an update by another transaction. T1 reads a row, T2 updates and commits it, T1 reads again and gets different data. **Solution**: Use `Repeatable Read` or `Serializable`.

  - **Phantom Read**: A query returns a different set of rows when re-executed because another transaction inserted/deleted matching rows.Example: T1 runs a query with a condition; T2 inserts a new matching row; T1 reruns and sees new row. **Solution**: Use `Serializable`, or databases supporting MVCC (like PostgreSQL or Oracle).

- **Durability**: Once a transaction is committed, it remains so, even in the event of a system failure.
### Distributed Transaction Protocols & Patterns

#### 1. Two-Phase Commit (2PC)

**Goal:**  
Ensure all participants in a distributed transaction either all commit or all roll back.

**Roles:**
- **Coordinator** — orchestrates the commit.
- **Participants (Resource Managers)** — e.g., databases, queues.

**Phases:**
1. **Prepare phase**  
   - Coordinator → Participants: *"Can you commit?"*  
   - Participants:  
     - Validate transaction feasibility (constraints, locks).  
     - If OK → reply **YES** (and lock resources so they can commit later).  
     - If not OK → reply **NO**.
2. **Commit/Abort phase**  
   - If **all YES** → Coordinator sends **COMMIT** to all.  
   - If **any NO** → Coordinator sends **ROLLBACK** to all.

**Pros:**
- Strong consistency.
- Simple to reason about.

**Cons:**
- **Blocking** — If coordinator crashes after prepare but before commit, participants wait indefinitely.
- Locks held across prepare → commit can hurt performance.

---

#### 2. Three-Phase Commit (3PC)

**Goal:**  
Reduce 2PC blocking by adding a pre-commit phase.

**Phases:**
1. **Can Commit**  
   - Same as 2PC’s prepare phase — ask if ready.
2. **Pre-Commit**  
   - If all **YES**: Coordinator sends **PRE-COMMIT** to participants.  
   - Participants acknowledge, enter a state where they can commit without coordinator.
3. **Do Commit**  
   - Coordinator sends **COMMIT**.  
   - If coordinator fails, participants can still commit safely after a timeout (based on pre-commit state).

**Pros:**
- Less blocking than 2PC.
- Participants can make progress after coordinator failure.

**Cons:**
- Requires synchronous clocks and reliable network assumptions (rare in real-world WAN).
- More message overhead.

---

#### 3. XA Transactions

**Goal:**  
Provide a standard API for distributed transactions across multiple resource managers.

**Key Points:**
- Defined by **X/Open XA** spec.
- Involves:
  - **Application** — business logic.
  - **Transaction Manager (TM)** — controls transaction boundaries.
  - **Resource Managers (RM)** — e.g., databases, message brokers.

**Flow:**
1. Application starts transaction (via TM).
2. Application interacts with multiple RMs.
3. TM calls RMs using XA API to prepare/commit.
4. Under the hood, TM uses **2PC** protocol (almost always).

**Important:**  
XA is **not** a commit algorithm — it’s a coordination API/spec. But in practice, **XA + 2PC** is the norm.

#### BASE Properties
BASE stands for Basically Available, Soft state, and Eventually consistent. These properties are common in distributed systems and NoSQL databases:
- **Basically Available**: The system guarantees availability, even in the presence of partial failures.
- **Soft State**: The state of the system may change over time, even without input, due to eventual consistency.
- **Eventually Consistent**: The system will become consistent over time, given that no new updates are made.


| Feature                | ACID                                                                                     | BASE                                                                                     |
|------------------------|------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| **Definition**         | Ensures reliable transactions with strong consistency and integrity.                     | Focuses on availability and eventual consistency in distributed systems.                 |
| **Consistency**        | Strong consistency; the database is always in a valid state after a transaction.         | Eventual consistency; the system becomes consistent over time.                          |
| **Availability**       | May sacrifice availability for consistency.                                              | Prioritizes availability, even during partial failures.                                  |
| **Data Integrity**     | High data integrity; suitable for critical applications like banking.                    | Lower data integrity; suitable for scalable systems like social media.                  |
| **Transaction Model**  | Transactions are all-or-nothing (atomic).                                                | Transactions may be partial or eventual.                                                |
| **Use Case**           | Ideal for OLTP systems requiring strict data accuracy.                                   | Ideal for distributed systems requiring high scalability and availability.              |
| **Examples**           | Relational databases like MySQL, PostgreSQL.                                             | NoSQL databases like Cassandra, DynamoDB.                                               |

---
### Normalization vs Denormalization

#### Purpose of Normalization
- Organize data to **reduce redundancy** and **improve integrity**.
- Avoid:
  - **Update anomalies**
  - **Insertion anomalies**
  - **Deletion anomalies**
- Achieved by splitting data into well-structured tables and defining relationships.

---

#### 1. First Normal Form (1NF)
**Rule:**
- Each column contains **atomic values** (no repeating groups, no arrays).
- Each row-column intersection holds **a single value**.
- Each record must be **unique** (primary key present).

**Example:**
❌ `Hobbies: [Reading, Swimming]`  
✅  
| ID | Hobby    |
|----|----------|
| 1  | Reading  |
| 1  | Swimming |

---

#### 2. Second Normal Form (2NF)
**Prerequisite:** Must be in **1NF**  
**Rule:**
- No **partial dependency** — non-key attributes must depend on the **whole** primary key.
- Applies only to tables with a **composite primary key**.

**Example:**
❌ `OrderID + ProductID → Quantity`, but `ProductName` depends only on `ProductID`.  
✅ Move product details to a separate **Product** table.

---

#### 3. Third Normal Form (3NF)
**Prerequisite:** Must be in **2NF**  
**Rule:**
- No **transitive dependency** — non-key attributes must depend **only** on the primary key.

**Example:**
❌ `StudentID → DepartmentID → DepartmentName`  
✅ Store `DepartmentID → DepartmentName` in a separate table.

---

#### 4. Boyce–Codd Normal Form (BCNF)
**Prerequisite:** Must be in **3NF**  
**Rule:**
- For **every functional dependency (X → Y)**, X must be a **superkey**.
- Stricter than 3NF — resolves anomalies that 3NF may allow.

---

#### 5. Fourth Normal Form (4NF)
**Prerequisite:** Must be in **BCNF**  
**Rule:**
- No **multi-valued dependencies** unless they are part of a candidate key.
- Prevents storing unrelated multi-valued facts in the same table.

**Example:**
If a teacher teaches multiple subjects **and** speaks multiple languages:  
- Store them in separate tables to avoid cross-product redundancy.

---

#### 6. Fifth Normal Form (5NF / Project-Join Normal Form)
**Prerequisite:** Must be in **4NF**  
**Rule:**
- No **join dependency** — table should not be reconstructable from smaller tables in any **non-trivial** way.
- Deals with complex relationships broken into **three or more** tables.

---

#### Quick Comparison Table

| Form  | Removes…                 | Focus Area                     |
|-------|--------------------------|---------------------------------|
| 1NF   | Repeating groups, arrays | Atomic data                     |
| 2NF   | Partial dependency       | Full key dependency             |
| 3NF   | Transitive dependency    | Direct PK dependency            |
| BCNF  | Any non-superkey FD      | Strict key dependency           |
| 4NF   | Multi-valued dependency  | No unrelated multi-values       |
| 5NF   | Join dependency          | Complex table reconstruction    |


Normalization is the process of organizing data to reduce redundancy and improve data integrity, while denormalization involves combining data to optimize read performance by reducing the number of joins.

| Feature                | Normalization                                                                 | Denormalization                                                              |
|------------------------|-------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Definition**         | Organizing data to reduce redundancy and improve data integrity.             | Combining data to reduce the number of joins and improve read performance.   |
| **Data Redundancy**    | Minimal redundancy; data is stored in separate, related tables.               | Increased redundancy; data is duplicated across tables.                      |
| **Performance**        | Optimized for write operations and data integrity.                            | Optimized for read operations and query performance.                         |
| **Complexity**         | Higher complexity due to multiple tables and relationships.                   | Lower complexity for queries but higher complexity for updates.              |
| **Use Case**           | Suitable for OLTP systems where data integrity and consistency are critical.  | Suitable for OLAP systems where fast read performance is required.           |
| **Storage**            | Requires less storage due to reduced redundancy.                              | Requires more storage due to duplicated data.                                |
| **Maintenance**        | Easier to maintain data integrity and consistency.                            | Harder to maintain consistency due to data duplication.                      |

---
### CAP Theorem

The **CAP Theorem**—also known as **Brewer’s Theorem**—states that in any distributed data system, it is **impossible to simultaneously guarantee** all three of the following properties:

- **C** — **Consistency** - Every read receives the most recent write or an error. Equivalent to strong consistency across nodes.
- **A** — **Availability** - Every request (read or write) receives a non-error response, without the guarantee that it contains the most recent write. The system is responsive even under stress.
- **P** — **Partition Tolerance** - The system continues to operate despite arbitrary partitioning (network failures/loss of connectivity between nodes). Must handle message loss or delay. In any real-world distributed system. So the real choice is between **Consistency** and **Availability**.


In practice, a system can **only guarantee two out of the three** at any given time. However with some complimenting strategies you can close to achieve the best of all for a given usecase. Remember the strongly and eventually consistant modes in case of Dynamodb.

#### Design Trade-offs: Choosing Two

| Type       | Properties Chosen | Trade-off |
|------------|-------------------|-----------|
| **CP**     | Consistency + Partition Tolerance | May reject requests during partition to preserve data integrity. |
| **CA**     | Consistency + Availability | Not realistic in distributed systems since network partitions are unavoidable. |
| **AP**     | Availability + Partition Tolerance | System may serve stale data or become eventually consistent. |

#### Design Perspective: What to Choose?

| Use Case | Recommended Trade-off | Reason |
|----------|------------------------|--------|
| **Banking/Financial Systems** | **CP** | Strong consistency is critical for correctness. |
| **Social Media Feeds**        | **AP** | Availability is prioritized; slight staleness is acceptable. |
| **E-commerce Carts**          | **AP** or **CP** | Depends on whether consistency (inventory) or uptime is more important. |
| **Real-time Messaging**       | **AP** | Users expect availability; some eventual consistency is acceptable. |

![](../cap.png)

> ⚠️ **Note**: CAP is a simplified model. In practice, systems also consider latency, throughput, durability, and more advanced consistency models like **Causal Consistency**, **Eventual Consistency**, and **Linearizability**.

#### Linearizability (Strong Consistency)
- Guarantees that all **operations appear to happen atomically and in a single, global order**.
- Once a write completes, all subsequent reads must return that value or a newer one.
- Operations appear **instantaneous** from the perspective of all clients.

**Example**:
- User A transfers $100 from Account X to Y.
- User B queries Account X and sees the debited balance immediately.
- No matter which server or region the users connect to, the order is preserved.

**Pros**:
- Predictable and intuitive behavior.
- Ideal for critical systems (e.g., banking, ledgers).

**Cons**:
- Slower performance due to coordination overhead.
- Difficult to scale globally.

#### Causal Consistency (Eventual Consistency)
- Guarantees that **causally related operations are seen in the same order by all nodes**.
- Independent operations may be seen in different orders by different nodes.

**Example**:
- Alice posts: "I love this product!"
- Bob replies: "Me too!"
- Everyone should see Alice’s post **before** Bob’s reply — because the reply is causally dependent.

**Pros**:
- Faster and more scalable.
- Sufficient for collaborative apps, chat, social networks.

**Cons**:
- Weaker guarantee: simultaneous updates may appear in different orders to different users.
- Not suitable for systems needing strong accuracy guarantees.

---

### Blob Storage
---
## Scalability and Performance
### Vertical and Horizontal Scaling

Scaling is a critical aspect of system design that ensures a system can handle increased load or demand. There are two primary types of scaling: vertical scaling and horizontal scaling.
Increase the power of a single machine.

- **Methods:** Add CPU, RAM, faster storage, GPUs, etc.
- **Pros:**
  - Simple to implement
  - Often no code change required
- **Cons:**
  - Hardware limits
  - Expensive
  - Single point of failure remains
- **Example:** Upgrading a database server from 8 cores to 64 cores

#### Vertical Scaling
Vertical scaling, also known as "scaling up," involves adding more resources (e.g., CPU, RAM, or storage) to a single machine. This approach is straightforward and often requires minimal changes to the application.

**Advantages:**
- Simplicity: Easier to implement and manage e.g. Postgres RDBMS Scaling up and down.
- No need for distributed systems: Avoids complexities like data partitioning and synchronization.
- Suitable for monolithic applications.

**Disadvantages:**
- Hardware limitations: There is a physical limit to how much a single machine can be upgraded.
- Single point of failure: If the machine fails, the entire system goes down.
- Cost: High-end hardware can be expensive.

#### Horizontal Scaling
Horizontal scaling, or "scaling out," involves adding more machines to distribute the load. This approach is commonly used in distributed systems and cloud environments.

**Advantages:**
- Scalability: Can handle virtually unlimited growth by adding more machines.
- Fault tolerance: Reduces the risk of a single point of failure.
- Cost efficiency: Commodity hardware can be used instead of expensive high-end machines.

**Disadvantages:**
- Complexity: Requires distributed systems, load balancing, and data partitioning.
- Consistency challenges: Ensuring data consistency across multiple nodes can be difficult.
- Network overhead: Communication between nodes can introduce latency.

#### Choosing Between Vertical and Horizontal Scaling
- **When to use vertical scaling:**
  - When the application is monolithic and not designed for distributed systems.
  - When the load is predictable and within the limits of a single machine.
  - When simplicity and quick implementation are priorities.

- **When to use horizontal scaling:**
  - When the system needs to handle unpredictable or massive growth.
  - When fault tolerance and high availability are critical.
  - When the application is designed as a distributed system.
  - Easy in Cloud infrastructure - Pay per use or Pay as you go.

#### Combining Vertical and Horizontal Scaling
In practice, systems often use a combination of vertical and horizontal scaling. For example:
- Start with vertical scaling for simplicity and quick deployment.
- Transition to horizontal scaling as the system grows and requires higher availability.

By understanding the trade-offs and leveraging efficient algorithms, you can design systems that scale effectively to meet user demands.

### Vertical vs Horizontal Scaling

Vertical scaling and horizontal scaling are two approaches to handle increased system load. Here's a comparison:

| Feature                | Vertical Scaling                                                              | Horizontal Scaling                                                             |
|------------------------|-------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Definition**         | Adding more resources (CPU, RAM, etc.) to a single machine.                  | Adding more machines to distribute the load.                                 |
| **Scalability**        | Limited by the hardware capacity of a single machine.                        | Virtually unlimited by adding more machines.                                 |
| **Fault Tolerance**    | Single point of failure; if the machine fails, the system goes down.         | Higher fault tolerance; failure of one machine does not affect the system.   |
| **Complexity**         | Simpler to implement and manage.                                             | Requires distributed systems, load balancing, and data partitioning.         |
| **Cost**               | High cost for high-end hardware.                                             | Cost-effective with commodity hardware.                                      |
| **Use Case**           | Suitable for monolithic applications with predictable loads.                 | Suitable for distributed systems with unpredictable or massive growth.       |

### Algorithmic Scaling

Algorithmic scaling plays a crucial role in ensuring that systems can handle increased load efficiently. By leveraging efficient algorithms and data structures, you can optimize performance and scalability, often reducing the need for additional hardware or resources.
![](../algoscaling.png)

**Big O Notation:**
Big O notation is used to describe the efficiency of an algorithm in terms of time and space complexity. Common complexities include:
- **O(1):** Constant time. Example: Hash table lookups.
- **O(log n):** Logarithmic time. Example: Binary search.
- **O(n):** Linear time. Example: Iterating through a list.
- **O(n log n):** Log-linear time. Example: Merge sort.
- **O(n^2):** Quadratic time. Example: Nested loops.

## 2️⃣ Distributed Scaling — The Scale Cube
(*You already know these, so just the headings for completeness*)

- **X-axis:** Horizontal duplication
- **Y-axis:** Functional decomposition
- **Z-axis:** Data partitioning

---

## 3️⃣ Additional Scaling Techniques (Beyond the Cube)

### 3.1 Scaling by Caching
Reduce load by storing frequently accessed results.  
**Examples:** CDN, Redis, in-memory caches

### 3.2 Scaling by Asynchrony & Queues
Smooth out load spikes by processing tasks asynchronously.  
**Examples:** Message brokers, event-driven architecture

### 3.3 Scaling by Algorithmic Efficiency
Reduce the amount of work or make it faster.  
**Examples:** Better data structures, batching, indexing

### 3.4 Scaling by Concurrency Model
Handle more work in parallel.  
**Examples:** Async I/O, multi-threading, actor model

### 3.5 Scaling Geographically
Deploy systems in multiple regions for latency and failover benefits.  
**Examples:** Multi-region deployments, edge computing

---

## Layered View

1. **First Layer** → Vertical scaling (make one box stronger)
2. **Second Layer** → Scale Cube (X, Y, Z axes for distribution)
3. **Third Layer** → Optimizations (caching, async, efficiency, concurrency, geo-distribution)

### Examples of Big O Notation in Java

#### O(1) - Constant Time
```java
public int getFirstElement(int[] array) {
    return array[0]; // Accessing the first element is constant time.
}
```

#### O(log n) - Logarithmic Time
```java
public int binarySearch(int[] array, int target) {
    int left = 0, right = array.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (array[mid] == target) {
            return mid; // Found the target.
        } else if (array[mid] < target) {
            left = mid + 1; // Search in the right half.
        } else {
            right = mid - 1; // Search in the left half.
        }
    }
    return -1; // Target not found.
}
```

#### O(n) - Linear Time
```java
public int findMax(int[] array) {
    int max = array[0];
    for (int num : array) {
        if (num > max) {
            max = num; // Update max if a larger number is found.
        }
    }
    return max;
}
```

#### O(n log n) - Log-Linear Time
```java
import java.util.Arrays;

public void sortArray(int[] array) {
    Arrays.sort(array); // Sorting an array using a comparison-based algorithm like Merge Sort.
}
```

#### O(n^2) - Quadratic Time
```java
public void printAllPairs(int[] array) {
    for (int i = 0; i < array.length; i++) {
        for (int j = 0; j < array.length; j++) {
            System.out.println(array[i] + ", " + array[j]); // Print all pairs.
        }
    }
}
```

#### O(2^n) - Exponential Time
```java
public int fibonacci(int n) {
    if (n <= 1) {
        return n; // Base case.
    }
    return fibonacci(n - 1) + fibonacci(n - 2); // Recursive calls.
}
```

#### O(n!) - Factorial Time
```java
public void generatePermutations(String str, String perm) {
    if (str.isEmpty()) {
        System.out.println(perm); // Print a permutation.
        return;
    }
    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        String remaining = str.substring(0, i) + str.substring(i + 1);
        generatePermutations(remaining, perm + ch); // Recursive call.
    }
}
```

### Load Balancers
### Rate Limiting
### Content Delivery Optimization
### Zero Downtime Deployment
---
## Common Design Patterns and Architecture
### Event-Driven Architecture
### Data Partitioning Strategies
### Eventual Consistency
### Leader Election
### Circuit Breaker Pattern
### Throttling and Backpressure
### Service Discovery
### Microservices
### Message Queues
---
## Monitoring, Resiliency, and Security
### Monitoring and Observability
### Data Compression
### Authentication and Authorization
### Data Backup and Recovery
### Chaos Engineering
---
## Development and Deployment
### Concurrency Control
### Immutable Infrastructure
### Blue-Green Deployment
---
## Theoretical Concepts
### Search Systems
---
## Data Processing
### Data Streaming
---
## Miscellaneous
### Rate Shaping
