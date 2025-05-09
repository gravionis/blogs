+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = 'System Design Interview Concepts'
+++

## Excerpt
Few Main concepts required for system design.

## Table of Contents
1. [Excerpt](#excerpt)
2. [Approach](#approach)
   - [Steps](#steps)
3. [Categories](#categories)
   - [Networking and Communication](#networking-and-communication)
   - [APIs and Integration](#apis-and-integration)
   - [Databases and Storage](#databases-and-storage)
   - [Scalability and Performance](#scalability-and-performance)
   - [System Design Patterns and Architecture](#system-design-patterns-and-architecture)
   - [Monitoring, Resiliency, and Security](#monitoring-resiliency-and-security)
   - [Development and Deployment](#development-and-deployment)
   - [Theoretical Concepts](#theoretical-concepts)
   - [Data Processing](#data-processing)
   - [Miscellaneous](#miscellaneous)

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

### Steps:
1. **Understand your use case**  
   - Clearly define the problem and its requirements.

2. **Ask the right questions**  
   - Gather Necessary details, NO assumptions.

3. **Decide the modules**  
   - Break the big problem into smaller, manageable parts (e.g., defining context boundaries).

4. **Design with key considerations**  
   - Address other critical "ilities":
     - **Availability**
     - **Reliability**
     - **Maintainability**
     - **Performance**
     - **Scalability**
     - **Cost-efficiency**
     - **Security**
     - **Flexibility**
     (Always remind yourself - everything fails)

# Networking and Communication
## Client Server Architecture
## IP Address
## DNS
## Proxy/Reverse Proxy
## Latency
## HTTP/HTTPS
## WebSockets
## Webhooks

# APIs and Integration
## APIs
## REST API
## GraphQL
## API Gateway
## Idempotency

# Databases and Storage
## Databases
## SQL vs NoSQL
## Database Indexing
## Replication
## Sharding
## Vertical Partitioning
## Caching

Caching is the process of storing frequently accessed data in a temporary storage layer to improve system performance and reduce latency. 

### Advantages of Caching

1. **Improved Performance**  
   - Reduces response time by serving data from faster storage layers (e.g., memory).  

2. **Reduced Latency**  
   - Minimizes delays in data retrieval, enhancing user experience.  

3. **Lower Database Load**  
   - Decreases the number of direct queries to the database, reducing resource usage.  

4. **Scalability**  
   - Helps handle increased traffic by offloading requests from the primary data source.  

5. **Cost Efficiency**  
   - Reduces operational costs by optimizing resource utilization.  

### Disadvantages of Caching

1. **Data Staleness**  
   - Cached data may become outdated if not properly invalidated or refreshed.  

2. **Complexity**  
   - Implementing and managing caching layers adds complexity to the system.  

3. **Cache Misses**  
   - If data is not found in the cache, it can lead to slower performance as the system falls back to the original data source.  

4. **Memory Overhead**  
   - Caching requires additional memory, which can increase infrastructure costs.  

5. **Consistency Challenges**  
   - Ensuring data consistency between the cache and the source of truth can be difficult.  

### Strategies

1. **Cache-Aside**  
   - The application checks the cache first. If the data is not found, it fetches from the database and updates the cache.  
   - Commonly used for read-heavy workloads.  

2. **Write-Through**  
   - Data is written to the cache and the database simultaneously.  
   - Ensures data consistency but may introduce higher write latency.  

3. **Write-Behind**  
   - Data is written to the cache first and asynchronously updated in the database.  
   - Improves write performance but risks data loss during failures.  

4. **Read-Through**  
   - The application interacts only with the cache. If the data is not in the cache, the cache fetches it from the database.  
   - Simplifies application logic but adds complexity to the caching layer.  

### Measuring Cache Effectiveness

1. **Calculate the Cache Hit Rate**  
   - Measure the percentage of requests served from the cache versus the total requests.  
   - A high hit rate indicates effective caching.  

2. **Analyze Cache Eviction Rate**  
   - Monitor how often data is evicted from the cache due to capacity limits.  
   - Optimize cache size and eviction policies to reduce unnecessary evictions.  

3. **Monitor Data Consistency**  
   - Ensure that cached data remains consistent with the source of truth (e.g., database).  
   - Use appropriate invalidation and expiration mechanisms.  

4. **Determine the Right Cache Expiration Time**  
   - Set expiration times based on data usage patterns and freshness requirements.  
   - Avoid stale data while minimizing unnecessary cache misses.

### Example Use Cases for Caching

1. **URL Shortener**  
   - Cache `ShortCode → URL` mappings.  
   - Strategy: LRU for frequently accessed URLs.

2. **User Profile Service**  
   - Cache user profiles with TTL for frequent reads.  
   - Challenge: Cache invalidation and consistency.

3. **Weather Forecast API**  
   - Cache responses based on `city+date`.  
   - Set TTL based on forecast freshness.

4. **Rate Limiter Service**  
   - Cache token bucket or sliding window counters per user.  
   - Use Redis or in-memory store with expiration.

5. **Product Catalog**  
   - Cache product details at edge/CDN.  
   - Strategy: Write-through or refresh-on-write.

6. **Twitter Feed**  
   - Cache user timelines and precompute recent tweets.  
   - Eviction policy: LRU or LFU.

7. **Geolocation Service**  
   - Cache frequently accessed IP ranges.  
   - Use TTL for DNS/IP lookups.

8. **Session Management**  
   - Store sessions in Redis with TTL.  
   - Trade-off: In-memory vs database storage.

9. **Distributed Cache System**  
   - Handle replication vs partitioning.  
   - Prevent hot keys and cache stampede.

10. **Online Code Editor**  
    - Cache user preferences and recent submissions.  
    - Use client-side and server-side caching.

### References

- [Cache Strategies - Medium](https://medium.com/@mmoshikoo/cache-strategies-996e91c80303)

## Denormalization
## Blob Storage

# Scalability and Performance
## Vertical and Horizontal Scaling
## Load Balancers
## Rate Limiting
## Content Delivery Optimization
## Zero Downtime Deployment

# System Design Patterns and Architecture
## Event-Driven Architecture
## Data Partitioning Strategies
## Eventual Consistency
## Leader Election
## Circuit Breaker Pattern
## Throttling and Backpressure
## Service Discovery
## Microservices
## Message Queues

# Monitoring, Resiliency, and Security
## Monitoring and Observability
## Data Compression
## Authentication and Authorization
## Data Backup and Recovery
## Chaos Engineering

# Development and Deployment
## Concurrency Control
## Immutable Infrastructure
## Blue-Green Deployment

# Theoretical Concepts
## CAP Theorem
## Search Systems

# Data Processing
## Data Streaming

# Miscellaneous
## Rate Shaping