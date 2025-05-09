+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = 'System Design Interview Concepts'
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

### Denormalization
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

### Algorithmic Scaling

Algorithmic scaling plays a crucial role in ensuring that systems can handle increased load efficiently. By leveraging efficient algorithms and data structures, you can optimize performance and scalability, often reducing the need for additional hardware or resources.

**Big O Notation:**
Big O notation is used to describe the efficiency of an algorithm in terms of time and space complexity. Common complexities include:
- **O(1):** Constant time. Example: Hash table lookups.
- **O(log n):** Logarithmic time. Example: Binary search.
- **O(n):** Linear time. Example: Iterating through a list.
- **O(n log n):** Log-linear time. Example: Merge sort.
- **O(n^2):** Quadratic time. Example: Nested loops.

**Examples of Efficient Algorithms:**
1. **Load Balancing:**
   - Use consistent hashing (O(log n)) to distribute requests evenly across servers.
   - Example: Distributing user sessions in a stateless web application.

2. **Data Partitioning:**
   - Use range-based or hash-based partitioning to divide data across nodes.
   - Example: Sharding a database to handle large datasets.

3. **Caching:**
   - Implement LRU (Least Recently Used) or LFU (Least Frequently Used) caching strategies to reduce database load.
   - Example: Caching frequently accessed user profiles.

4. **Search Systems:**
   - Use inverted indexes and binary search trees for efficient search operations.
   - Example: Full-text search in a document management system.

By understanding and applying these algorithmic principles, you can design systems that scale effectively to meet user demands.

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
### CAP Theorem
### Search Systems
---
## Data Processing
### Data Streaming
---
## Miscellaneous
### Rate Shaping