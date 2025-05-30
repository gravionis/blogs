+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = 'System Design Interview Concepts'
tags = ['Event Driven Architecture', 'Microservices', 'Interview']
+++

System design is a critical aspect of software engineering that involves creating scalable, reliable, and efficient systems. This document explores key concepts and strategies required for designing robust systems, including networking, databases, scalability, caching, and modern architectural patterns. It serves as a comprehensive guide for understanding the foundational and advanced principles of system design.

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
## Networking and Communication
### Client Server Architecture
### IP Address
### DNS
### Proxy/Reverse Proxy
### Latency
### HTTP/HTTPS
### WebSockets
### Webhooks
---
## APIs and Integration
### APIs
### REST API
### GraphQL
### API Gateway
### Idempotency

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
### SQL vs NoSQL
### Database Indexing
### Replication
### Sharding
### Vertical Partitioning
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

### Normalization vs Denormalization

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

### CAP Theorem
### CAP Theorem (Design Perspective)

The **CAP Theorem**—also known as **Brewer’s Theorem**—states that in any distributed data system, it is **impossible to simultaneously guarantee** all three of the following properties:

- **C** — **Consistency**
- **A** — **Availability**
- **P** — **Partition Tolerance**

In practice, a system can **only guarantee two out of the three** at any given time.

---

#### 🔺 The Three Properties

- **Consistency (C)**  
  Every read receives the most recent write or an error. Equivalent to strong consistency across nodes.

- **Availability (A)**  
  Every request (read or write) receives a non-error response, without the guarantee that it contains the most recent write. The system is responsive even under stress.

- **Partition Tolerance (P)**  
  The system continues to operate despite arbitrary partitioning (network failures/loss of connectivity between nodes). Must handle message loss or delay.

---

#### ⚙️ Design Trade-offs: Choosing Two

| Type       | Properties Chosen | Trade-off |
|------------|-------------------|-----------|
| **CP**     | Consistency + Partition Tolerance | May reject requests during partition to preserve data integrity. |
| **CA**     | Consistency + Availability | Not realistic in distributed systems since network partitions are unavoidable. |
| **AP**     | Availability + Partition Tolerance | System may serve stale data or become eventually consistent. |

> 💡 **Partition Tolerance is a must** in any real-world distributed system. So the real choice is between **Consistency** and **Availability**.

---

#### 🧱 Design Perspective: What to Choose?

| Use Case | Recommended Trade-off | Reason |
|----------|------------------------|--------|
| **Banking/Financial Systems** | **CP** | Strong consistency is critical for correctness. |
| **Social Media Feeds**        | **AP** | Availability is prioritized; slight staleness is acceptable. |
| **E-commerce Carts**          | **AP** or **CP** | Depends on whether consistency (inventory) or uptime is more important. |
| **Real-time Messaging**       | **AP** | Users expect availability; some eventual consistency is acceptable. |
![](../cap.png)

> ⚠️ **Note**: CAP is a simplified model. In practice, systems also consider latency, throughput, durability, and more advanced consistency models like **Causal Consistency**, **Eventual Consistency**, and **Linearizability**.
### Consistency Models: Linearizability vs Causal Consistency

#### 🔗 Linearizability (Strong Consistency)
- Guarantees that all **operations appear to happen atomically and in a single, global order**.
- Once a write completes, all subsequent reads must return that value or a newer one.
- Operations appear **instantaneous** from the perspective of all clients.

**Example**:
- User A transfers $100 from Account X to Y.
- User B queries Account X and sees the debited balance immediately.
- No matter which server or region the users connect to, the order is preserved.

✅ **Pros**:
- Predictable and intuitive behavior.
- Ideal for critical systems (e.g., banking, ledgers).

❌ **Cons**:
- Slower performance due to coordination overhead.
- Difficult to scale globally.

---

#### 🔁 Causal Consistency (Weaker Consistency)
- Guarantees that **causally related operations are seen in the same order by all nodes**.
- Independent operations may be seen in different orders by different nodes.

**Example**:
- Alice posts: "I love this product!"
- Bob replies: "Me too!"
- Everyone should see Alice’s post **before** Bob’s reply — because the reply is causally dependent.

✅ **Pros**:
- Faster and more scalable.
- Sufficient for collaborative apps, chat, social networks.

❌ **Cons**:
- Weaker guarantee: simultaneous updates may appear in different orders to different users.
- Not suitable for systems needing strong accuracy guarantees.

---


### Blob Storage
---
## Scalability and Performance
### Vertical and Horizontal Scaling

Scaling is a critical aspect of system design that ensures a system can handle increased load or demand. There are two primary types of scaling: vertical scaling and horizontal scaling.

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