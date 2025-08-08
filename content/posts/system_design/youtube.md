+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = 'Youtube System Design Interview'
tags = ['Youtube', 'Interview']
+++

This document provides a comprehensive, step-by-step breakdown of how to architect a YouTube-scale system, covering requirements, high-level architecture, scaling strategies, microservices patterns, storage, processing pipelines, monitoring, security, and more. The goal is to demonstrate a practical, modern approach to building and scaling a global video platform.

## Technical & Business Requirements

The **platform** must _enable_ **users** to _upload_, _manage_, and _stream_ **video content** at **scale**, _supporting_ a seamless **experience** across **devices** and **geographies**. **Users** should _be able to create_ personal or branded **channels**, _publish_ **videos** with **metadata** (**title**, **description**, **tags**), and _interact_ with **content** through **likes**, **comments**, and **shares**. The **system** must _support_ **user authentication**, personalized **recommendations**, and real-time **notifications** for **subscriptions** and **interactions**. **Search functionality** should _allow_ **users** to _discover_ **content** based on **relevance**, **popularity**, and **preferences**.

From a **business perspective**, the **system** must _ensure_ high **availability**, **scalability**, and **performance** to _support_ billions of daily **interactions**. It should _enable_ **content moderation workflows** to _maintain_ **community standards** and _comply_ with legal **regulations**. **Analytics capabilities** must _provide_ **insights** into **user engagement**, **video performance**, and **platform health**. The **architecture** should _support_ modular **growth**, _allowing_ **teams** to independently _develop_ and _deploy_ **features** aligned with **business capabilities** such as **video management**, **user engagement**, and **content discovery**.
# Nouns and Verbs from Video Platform Requirements

## Nouns

| Noun | Category | Description |
|------|----------|-------------|
| platform | System | The main video streaming system |
| users | People | End users of the platform |
| video content | Media | Videos uploaded to the platform |
| scale | Concept | Large-scale operations |
| experience | Concept | User interaction quality |
| devices | Hardware | User devices (mobile, desktop, etc.) |
| geographies | Location | Global regions |
| channels | Feature | User/brand content channels |
| videos | Media | Individual video files |
| metadata | Data | Video information (title, description, tags) |
| title | Data | Video title |
| description | Data | Video description |
| tags | Data | Video categorization tags |
| content | Media | General platform content |
| likes | Interaction | User approval actions |
| comments | Interaction | User feedback/discussion |
| shares | Interaction | Content sharing actions |
| system | Infrastructure | Platform technical system |
| user authentication | Security | Login/identity verification |
| recommendations | Feature | Personalized content suggestions |
| notifications | Feature | Real-time user alerts |
| subscriptions | Feature | Channel following system |
| interactions | Activity | User engagement activities |
| search functionality | Feature | Content discovery tool |
| relevance | Algorithm | Search ranking factor |
| popularity | Algorithm | Content popularity metric |
| preferences | User Data | User personal choices |
| business perspective | Viewpoint | Commercial considerations |
| availability | Performance | System uptime |
| scalability | Performance | Growth handling capability |
| performance | Quality | System speed/efficiency |
| content moderation workflows | Process | Content review processes |
| community standards | Policy | Platform usage rules |
| regulations | Legal | Legal compliance requirements |
| analytics capabilities | Feature | Data analysis tools |
| insights | Data | Business intelligence |
| user engagement | Metrics | User activity measurements |
| video performance | Metrics | Video success metrics |
| platform health | Metrics | System status indicators |
| architecture | Infrastructure | System design structure |
| growth | Business | Platform expansion |
| teams | People | Development teams |
| features | Functionality | Platform capabilities |
| business capabilities | Concept | Core business functions |
| video management | Capability | Video handling processes |
| user engagement | Capability | User interaction systems |
| content discovery | Capability | Content finding mechanisms |

## Verbs

| Verb | Type | Usage Context |
|------|------|---------------|
| enable | Transitive | Allow functionality |
| upload | Transitive | Transfer video files |
| manage | Transitive | Control/organize content |
| stream | Transitive | Deliver video content |
| supporting | Present Participle | Providing assistance |
| create | Transitive | Make new channels |
| publish | Transitive | Make videos available |
| interact | Intransitive | Engage with content |
| support | Transitive | Provide functionality |
| allow | Transitive | Permit actions |
| discover | Transitive | Find content |
| ensure | Transitive | Guarantee outcomes |
| enable | Transitive | Make possible |
| maintain | Transitive | Keep standards |
| comply | Intransitive | Follow regulations |
| provide | Transitive | Supply insights |
| support | Transitive | Enable growth |
| allowing | Present Participle | Permitting teams |
| develop | Transitive | Create features |
| deploy | Transitive | Release features |

Key DDD Concepts Identified:

- Entities: Things with identity that change over time (Users, Videos, Channels, Comments)
- Value Objects: Immutable descriptors (Metadata, Tags, Preferences)
- Domain Events: Significant business occurrences (VideoUploaded, UserSubscribed)
- Domain Services: Business logic that doesn't belong to entities (Search, Moderation)
- Aggregates: Consistency boundaries (Video + Metadata, User + Channels)

8 Bounded Contexts emerged naturally from the requirements:

- User Management
- Content Management
- Engagement
- Discovery
- Notification
- Analytics
- Moderation
- Content Delivery

Ubiquitous Language: Defined key terms that should be used consistently across the development team and business stakeholders.
This DDD analysis provides a much stronger foundation for:

Microservices architecture design
- Team organization
- API boundaries
- Database design
- Business rule implementation


## 1. Requirements Gathering

### Functional Requirements
- **Video Upload**: Users can upload videos (multiple formats, sizes up to 10GB)
- **Video Streaming**: Users can watch videos with adaptive bitrate streaming
- **Video Search**: Search videos by title, description, tags, channel
- **User Management**: Registration, authentication, profiles, subscriptions
- **Social Features**: Comments, likes/dislikes, sharing, playlists
- **Channel Management**: Create channels, manage content, analytics
- **Content Moderation**: Automated and manual content review
- **Notifications**: Subscription updates, comment replies, trending content

### Non-Functional Requirements
#### User Scale
- **Total registered users:** 2+ billion
- **Daily active users (DAU):** 500+ million
- **Monthly active users (MAU):** 1.5+ billion
- **Concurrent users (peak):** 50+ million

#### System Throughput
- **Video uploads:** 500+ hours of content uploaded per minute
- **Video consumption:** 1+ billion hours watched daily
- **Search queries:** 1+ billion queries per day

#### Availability & Reliability
- **Uptime SLA:** 99.9% globally
- **CAP Theorem priority:**
  - Prioritize **Availability** and **Partition Tolerance**
  - Accept **Eventual Consistency** where applicable

#### Performance & Latency
- **Video start time:** < 2 seconds globally
- **Search results latency:** < 300 milliseconds
- **Upload processing time:** Variable (based on video size and format)
- **Page load time (95th percentile):** < 1 second

#### Consistency & Data Integrity
- **User authentication & billing:** Strong consistency
- **Social features (likes, comments, views):** Eventually consistent
- **Content metadata updates:** Eventually consistent

#### Storage & Data Management
- **Video storage:** Exabyte-scale, globally distributed
- **Metadata storage:** Highly available, low-latency key-value store
- **Backup & disaster recovery:** Geo-redundant with RPO < 1 hour

#### Bandwidth & Traffic
- **Daily data transfer:** Petabyte-scale
- **Peak bandwidth usage:** 100+ Tbps globally
- **CDN usage:** Aggressive caching and edge delivery for video content

#### Security & Compliance
- **Data encryption:** At rest and in transit
- **Access control:** Role-based and region-aware
- **Compliance:** GDPR, CCPA, and other regional regulations

### Scale Estimation
- **Users**: 2.7B monthly active users
- **Videos**: 720,000 hours uploaded daily
- **Storage**: 1PB+ new content daily
- **Bandwidth**: 30PB+ daily egress traffic
- **QPS**: 1M+ concurrent video streams

## 2. High-Level Architecture

```
[CDN Layer] → [Load Balancers] → [API Gateway] → [Microservices]
                                                      ↓
[Message Queue] ← [Video Processing Pipeline] ← [Object Storage]
                                                      ↓
[Search Engine] ← [Metadata Services] → [Analytics Pipeline]
```

### Core Components
1. **API Gateway** - Request routing, authentication, rate limiting
2. **Video Upload Service** - Handle video ingestion and initial processing
3. **Video Processing Pipeline** - Transcoding, thumbnail generation, ML analysis
4. **Video Streaming Service** - Adaptive bitrate delivery
5. **Metadata Service** - Video information, user data, social interactions
6. **Search Service** - Video discovery and recommendation
7. **User Service** - Authentication, profiles, subscriptions
8. **Analytics Service** - View tracking, performance metrics
9. **Notification Service** - Real-time updates and alerts

## 2a. Microservice Decomposition & Hexagonal Architecture (Chris Richardson)

### Decomposition Strategies (from "Microservices Patterns")
- **By Business Capability**: Decompose services around business domains (e.g., Video Management, User Management, Social Interactions, Analytics).
- **By Subdomain (DDD)**: Identify core, supporting, and generic subdomains (e.g., Video Processing as core, Notification as supporting).
- **By Transaction Boundary**: Services should own their data and transactional boundaries (e.g., Video Upload and Processing as separate services).
- **By Team Ownership**: Align services with team boundaries for independent delivery.

### Hexagonal Architecture (Ports & Adapters)
- **Service Core**: Business logic is isolated from external systems.
- **Ports**: Define interfaces for driving (API, UI) and driven (DB, messaging, external APIs) adapters.
- **Adapters**: Implement ports for REST, gRPC, Kafka, databases, etc.
- **Benefits**: Improves testability, flexibility, and separation of concerns.

#### Example: Video Upload Service (Hexagonal)
- **Core**: Handles upload validation, metadata extraction, and orchestration.
- **Inbound Adapter**: REST API for receiving uploads.
- **Outbound Adapters**: Kafka producer for events, S3 adapter for storage, DB adapter for metadata.

### Additional Patterns from the Book
- **API Composition**: Aggregate data from multiple services for UI.
- **Database per Service**: Each service owns its schema.
- **Saga Pattern**: Manage distributed transactions (e.g., video upload workflow).
- **CQRS**: Separate read/write models for scalability.
- **Event Sourcing**: Persist state changes as events for auditability.

## 3. Scale Cube Application for 10x Growth

### X-Axis Scaling (Horizontal Duplication)
- **Load Balancers**: Deploy multiple tiers (L4/L7) with auto-scaling
- **API Gateway Clusters**: Regional deployment with intelligent routing
- **Microservice Replicas**: Auto-scaling based on CPU, memory, and queue depth
- **Database Read Replicas**: Multiple read-only instances per region

### Y-Axis Scaling (Functional Decomposition)
- **Service Decomposition**:
  - Upload Service → Video Ingestion + Metadata Extraction + Storage
  - User Service → Auth + Profile + Subscription + Preferences
  - Social Service → Comments + Likes + Sharing + Community
- **Database Decomposition**: Separate DBs for videos, users, analytics, social
- **Event-Driven Architecture**: Loose coupling via message queues

### Z-Axis Scaling (Data Partitioning)
- **Video Sharding**: By video ID hash, geographic region, or creator
- **User Sharding**: By user ID hash or geographic region
- **Temporal Sharding**: Hot data (recent) vs cold data (archived)
- **Content-Based Sharding**: By video category, language, or popularity

## 4. Microservices Design Patterns

### Service Patterns
- **API Gateway Pattern**: Single entry point with cross-cutting concerns
- **Service Registry & Discovery**: Consul/Eureka for service location
- **Circuit Breaker**: Hystrix for fault tolerance and cascading failure prevention
- **Bulkhead**: Resource isolation between services
- **Retry with Exponential Backoff**: Resilient inter-service communication

### Data Patterns
- **Database per Service**: Each microservice owns its data
- **Saga Pattern**: Distributed transactions for video upload workflow
- **CQRS**: Separate read/write models for video metadata and analytics
- **Event Sourcing**: Audit trail for user actions and video lifecycle

### Communication Patterns
- **Asynchronous Messaging**: Kafka for video processing pipeline
- **Request-Response**: HTTP/gRPC for real-time user interactions
- **Publish-Subscribe**: Event notifications for subscriptions
- **Message Routing**: Content-based routing for different video types

- **Hexagonal Architecture**: Each service is designed using ports and adapters, isolating business logic from infrastructure.
- **Decomposition by Business Capability**: Services are split by domain, following DDD and team boundaries.
- **Saga Pattern**: Used for workflows like video upload and processing.
- **CQRS & Event Sourcing**: Applied for scalability and auditability.

## 5. Event-Driven Architecture (EDA)

### Event Streaming Platform
```
Video Upload → [Event Producer] → [Kafka Topics] → [Event Consumers] → Processing Services
```

### Core Events
- **VideoUploadedEvent**: Triggers transcoding pipeline
- **VideoProcessedEvent**: Updates metadata and makes video available
- **UserActionEvent**: Likes, comments, views for recommendation engine
- **SubscriptionEvent**: Channel subscription/unsubscription
- **ModerationEvent**: Content review results

### Event Patterns
- **Event Sourcing**: Store all state changes as events
- **CQRS**: Separate command and query responsibility
- **Event Choreography**: Services react to events autonomously
- **Event Orchestration**: Central coordinator for complex workflows

## 6. CAP Theorem Considerations

### Design Decisions
- **Partition Tolerance**: Always required in distributed system
- **Availability vs Consistency Trade-offs**:
  - **AP Systems**: Video streaming, comments, likes (eventual consistency)
  - **CP Systems**: User authentication, payment processing
  - **CA Systems**: Single-region components with strong consistency

### Implementation Strategy
- **Multi-Region Deployment**: Handle network partitions
- **Eventual Consistency**: Social features can tolerate temporary inconsistency
- **Strong Consistency**: Critical operations like user authentication
- **Conflict Resolution**: Last-writer-wins, vector clocks for concurrent updates

## 7. Storage Architecture

### Video Storage
- **Object Storage**: S3/GCS for raw and processed video files
- **CDN**: CloudFront/CloudFlare for global content delivery
- **Storage Tiers**: Hot (recent), warm (popular), cold (archived)
- **Compression**: AV1 codec for 30% bandwidth savings

### Metadata Storage
- **Relational Database**: PostgreSQL for structured data (users, videos)
- **Document Database**: MongoDB for flexible schemas (comments, analytics)
- **Graph Database**: Neo4j for social relationships and recommendations
- **Cache Layer**: Redis for frequently accessed data

### Search Index
- **Elasticsearch**: Full-text search for videos, channels, playlists
- **Vector Database**: Pinecone for ML-based video recommendations
- **Real-time Indexing**: Stream processing for immediate search availability

## 8. Video Processing Pipeline

### Processing Stages
1. **Ingestion**: Upload validation, virus scanning, metadata extraction
2. **Transcoding**: Multiple resolutions, formats, and bitrates
3. **AI Processing**: Content analysis, thumbnail generation, closed captions
4. **Quality Check**: Automated quality assessment and optimization
5. **Distribution**: CDN upload and cache warming

### Technologies
- **Message Queue**: Apache Kafka for pipeline orchestration
- **Container Orchestration**: Kubernetes for scalable processing
- **Workflow Engine**: Apache Airflow for complex processing workflows
- **ML Platform**: TensorFlow Serving for content analysis

## 9. Scaling Strategies for 10x Growth

### Infrastructure Scaling
- **Multi-Cloud**: AWS, GCP, Azure for redundancy and cost optimization
- **Edge Computing**: Process videos closer to users
- **Serverless**: Lambda/Cloud Functions for variable workloads
- **Auto-scaling**: Predictive scaling based on usage patterns

### Performance Optimization
- **Caching Strategy**: 
  - L1: Browser cache (static content)
  - L2: CDN cache (popular videos)
  - L3: Application cache (metadata)
  - L4: Database cache (query results)

### Data Management
- **Data Archiving**: Move old content to cheaper storage tiers
- **Data Compression**: Advanced codecs and compression algorithms
- **Smart Prefetching**: ML-based content prediction and caching
- **Geographic Optimization**: Content placement based on user location

## 10. Monitoring and Observability

### Metrics
- **Golden Signals**: Latency, traffic, errors, saturation
- **Business Metrics**: Video start failures, buffering ratio, user engagement
- **Infrastructure Metrics**: CPU, memory, network, storage utilization

### Tools
- **Monitoring**: Prometheus, Grafana, DataDog
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana)
- **Tracing**: Jaeger, Zipkin for distributed tracing
- **Alerting**: PagerDuty for incident management

## 11. Security Considerations

### Content Security
- **DRM**: Widevine, FairPlay for premium content protection
- **Content Filtering**: ML-based inappropriate content detection
- **Access Control**: JWT tokens, OAuth 2.0, rate limiting

### Infrastructure Security
- **Network Security**: VPC, security groups, WAF
- **Encryption**: TLS in transit, AES-256 at rest
- **Secrets Management**: HashiCorp Vault, AWS Secrets Manager
- **Compliance**: GDPR, COPPA, regional data protection laws

## 12. Cost Optimization

### Storage Optimization
- **Intelligent Tiering**: Automatic movement between storage classes
- **Deduplication**: Remove duplicate video segments
- **Compression**: Advanced codecs (AV1, H.265) for bandwidth savings
- **Regional Optimization**: Store content closer to primary audience

### Compute Optimization
- **Spot Instances**: Use for batch processing jobs
- **Right-sizing**: ML-based instance size recommendations
- **Reserved Capacity**: Long-term commitments for predictable workloads
- **Serverless**: Pay-per-use for variable workloads

## 13. Disaster Recovery and Business Continuity

### Backup Strategy
- **Multi-Region Replication**: Critical data replicated across regions
- **Point-in-Time Recovery**: Database snapshots and transaction logs
- **Content Backup**: Multiple copies of popular content

### Recovery Procedures
- **RTO (Recovery Time Objective)**: 15 minutes for critical services
- **RPO (Recovery Point Objective)**: 5 minutes for user data
- **Failover Automation**: Automated traffic rerouting during outages
- **Chaos Engineering**: Regular disaster simulations

## 14. Key Principles and Laws Applied

### Performance Laws
- **Little's Law**: Queue length = arrival rate × response time
- **Amdahl's Law**: Parallel processing limitations
- **Universal Scalability Law**: Overhead of coordination in distributed systems

### Design Principles
- **Single Responsibility**: Each service has one clear purpose
- **Open/Closed**: Services open for extension, closed for modification
- **Dependency Inversion**: Depend on abstractions, not concretions
- **Fail Fast**: Immediate error detection and reporting

### Reliability Patterns
- **Bulkhead**: Isolate resources to prevent cascading failures
- **Circuit Breaker**: Prevent calls to failing services
- **Timeout**: Set maximum wait times for all operations
- **Idempotency**: Safe to retry operations multiple times

### Additional Laws and Principles
- **Murphy's Law**: "Anything that can go wrong will go wrong." Design for failure and recovery.
- **Conway's Law**: System design mirrors the communication structure of the organization.
- **Occam's Razor**: Prefer the simplest solution that works.
- **Robustness Principle (Postel's Law)**: "Be conservative in what you send, be liberal in what you accept."
- **Law of Demeter**: Minimize coupling by only interacting with immediate collaborators.
- **Hofstadter's Law**: "It always takes longer than you expect, even when you take into account Hofstadter's Law."
- **Pareto Principle (80/20 Rule)**: 80% of effects come from 20% of causes; optimize for the critical path.
- **Peter Principle**: In hierarchical organizations, people tend to be promoted to their level of incompetence (impacts team/org design).
- **Gall's Law**: A complex system that works is invariably found to have evolved from a simple system that worked.

## 15. Database Design

### User Service Database
```sql
-- Users table
CREATE TABLE users (
    user_id BIGINT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    last_login TIMESTAMP
);

-- Channels table
CREATE TABLE channels (
    channel_id BIGINT PRIMARY KEY,
    user_id BIGINT REFERENCES users(user_id),
    channel_name VARCHAR(100) NOT NULL,
    description TEXT,
    subscriber_count BIGINT DEFAULT 0,
    created_at TIMESTAMP DEFAULT NOW()
);

-- Subscriptions table (sharded by user_id)
CREATE TABLE subscriptions (
    subscription_id BIGINT PRIMARY KEY,
    subscriber_id BIGINT REFERENCES users(user_id),
    channel_id BIGINT REFERENCES channels(channel_id),
    subscribed_at TIMESTAMP DEFAULT NOW(),
    UNIQUE(subscriber_id, channel_id)
);
```

### Video Service Database
```sql
-- Videos table (sharded by video_id hash)
CREATE TABLE videos (
    video_id BIGINT PRIMARY KEY,
    channel_id BIGINT NOT NULL,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    duration INTEGER, -- in seconds
    view_count BIGINT DEFAULT 0,
    like_count BIGINT DEFAULT 0,
    dislike_count BIGINT DEFAULT 0,
    upload_time TIMESTAMP DEFAULT NOW(),
    processing_status ENUM('uploading', 'processing', 'ready', 'failed'),
    visibility ENUM('public', 'private', 'unlisted')
);

-- Video metadata table
CREATE TABLE video_metadata (
    video_id BIGINT PRIMARY KEY REFERENCES videos(video_id),
    file_size BIGINT,
    codec VARCHAR(50),
    resolution VARCHAR(20),
    bitrate INTEGER,
    thumbnail_url VARCHAR(500),
    tags TEXT[] -- PostgreSQL array for tags
);

-- Comments table (sharded by video_id)
CREATE TABLE comments (
    comment_id BIGINT PRIMARY KEY,
    video_id BIGINT NOT NULL,
    user_id BIGINT NOT NULL,
    parent_comment_id BIGINT, -- for replies
    content TEXT NOT NULL,
    like_count INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT NOW()
);
```

## 16. API Design

### REST API Endpoints

#### Video Operations
```http
# Upload video
POST /api/v1/videos
Content-Type: multipart/form-data

# Get video details
GET /api/v1/videos/{videoId}

# Update video metadata
PUT /api/v1/videos/{videoId}

# Delete video
DELETE /api/v1/videos/{videoId}

# Search videos
GET /api/v1/videos/search?q={query}&limit={limit}&offset={offset}

# Get trending videos
GET /api/v1/videos/trending?category={category}&region={region}
```

#### User Operations
```http
# User registration
POST /api/v1/users/register

# User login
POST /api/v1/users/login

# Get user profile
GET /api/v1/users/{userId}

# Subscribe to channel
POST /api/v1/users/{userId}/subscriptions/{channelId}

# Get user subscriptions
GET /api/v1/users/{userId}/subscriptions
```

#### Social Operations
```http
# Like/Unlike video
POST /api/v1/videos/{videoId}/like
DELETE /api/v1/videos/{videoId}/like

# Add comment
POST /api/v1/videos/{videoId}/comments

# Get comments
GET /api/v1/videos/{videoId}/comments?limit={limit}&offset={offset}

# Reply to comment
POST /api/v1/comments/{commentId}/replies
```

### GraphQL Schema (Alternative)
```graphql
type Video {
  id: ID!
  title: String!
  description: String
  duration: Int!
  viewCount: Int!
  likeCount: Int!
  uploadTime: String!
  channel: Channel!
  comments(first: Int, after: String): CommentConnection
}

type Channel {
  id: ID!
  name: String!
  subscriberCount: Int!
  videos(first: Int, after: String): VideoConnection
}

type Query {
  video(id: ID!): Video
  searchVideos(query: String!, first: Int, after: String): VideoConnection
  trendingVideos(category: String, region: String): [Video!]!
}

type Mutation {
  uploadVideo(input: VideoInput!): Video
  likeVideo(videoId: ID!): Video
  addComment(videoId: ID!, content: String!): Comment
}
```

## 17. Caching Strategy

### Multi-Level Caching
```yaml
# Level 1: Browser Cache
- Static assets: 1 year
- Video thumbnails: 1 week
- API responses: 5 minutes

# Level 2: CDN Cache (CloudFlare/CloudFront)
- Video segments: 1 day
- Thumbnails: 1 week
- API responses: 1 minute

# Level 3: Application Cache (Redis)
- Popular video metadata: 1 hour
- User sessions: 24 hours
- Search results: 15 minutes
- Trending videos: 30 minutes

# Level 4: Database Query Cache
- Complex analytics queries: 5 minutes
- User profile data: 30 minutes
- Channel information: 1 hour
```

### Cache Invalidation Strategy
- **Time-based**: TTL for most cached data
- **Event-based**: Invalidate on video updates, user actions
- **Version-based**: Cache keys include version numbers
- **Write-through**: Update cache and database simultaneously
- **Write-behind**: Async cache updates for non-critical data

## 18. Message Queue Architecture

### Kafka Topic Design
```yaml
# Video Processing Topics
video-upload-events:
  partitions: 100
  replication-factor: 3
  retention: 7 days

video-transcoding-jobs:
  partitions: 50
  replication-factor: 3
  retention: 3 days

video-ready-events:
  partitions: 100
  replication-factor: 3
  retention: 30 days

# User Activity Topics
user-view-events:
  partitions: 200
  replication-factor: 3
  retention: 90 days

user-interaction-events:
  partitions: 100
  replication-factor: 3
  retention: 30 days

# Notification Topics
subscription-notifications:
  partitions: 50
  replication-factor: 3
  retention: 7 days
```

### Event Schema (Avro)
```json
{
  "type": "record",
  "name": "VideoUploadEvent",
  "fields": [
    {"name": "videoId", "type": "string"},
    {"name": "userId", "type": "string"},
    {"name": "channelId", "type": "string"},
    {"name": "filename", "type": "string"},
    {"name": "fileSize", "type": "long"},
    {"name": "contentType", "type": "string"},
    {"name": "uploadTimestamp", "type": "long"},
    {"name": "metadata", "type": {"type": "map", "values": "string"}}
  ]
}
```

## 19. Load Balancing Strategy

### Geographic Load Balancing
```yaml
# DNS-based routing
Global Load Balancer:
  - US-East: 40% traffic
  - US-West: 20% traffic
  - Europe: 25% traffic
  - Asia-Pacific: 15% traffic

# Regional Load Balancers
Regional LB (L7):
  - Path-based routing: /api/upload → Upload Service
  - Header-based routing: User-Agent → Mobile/Web Service
  - Weighted routing: Canary deployments

# Service Load Balancers (L4)
Service Discovery:
  - Health checks every 30 seconds
  - Circuit breaker: 5 failures in 60 seconds
  - Load balancing algorithms: Weighted round-robin
```

### Auto-scaling Configuration
```yaml
# Horizontal Pod Autoscaler (Kubernetes)
Video Upload Service:
  minReplicas: 10
  maxReplicas: 100
  targetCPUUtilization: 70%
  targetMemoryUtilization: 80%
  scaleUpStabilization: 60s
  scaleDownStabilization: 300s

Video Streaming Service:
  minReplicas: 50
  maxReplicas: 500
  targetCPUUtilization: 60%
  customMetrics:
    - concurrent_streams_per_pod: 1000
```

## 20. Monitoring and Alerting

### Key Metrics Dashboard
```yaml
# Golden Signals
Latency:
  - Video start time: P50, P95, P99
  - API response time: P50, P95, P99
  - Upload processing time: P50, P95, P99

Traffic:
  - Requests per second by endpoint
  - Concurrent video streams
  - Upload requests per minute

Errors:
  - HTTP error rates (4xx, 5xx)
  - Video processing failures
  - Database connection errors

Saturation:
  - CPU utilization across services
  - Memory usage patterns
  - Queue depth in Kafka topics
  - Storage utilization
```

### Alert Rules
```yaml
# Critical Alerts (PagerDuty)
Video Start Failure Rate > 1%:
  severity: critical
  notification: immediate

API Error Rate > 5%:
  severity: critical
  notification: immediate

Database Connection Pool > 90%:
  severity: critical
  notification: immediate

# Warning Alerts (Slack)
Upload Processing Time > P95:
  severity: warning
  notification: 5-minute delay

CDN Cache Hit Rate < 85%:
  severity: warning
  notification: 10-minute delay
```

## Conclusion

This comprehensive YouTube system design demonstrates how to architect a massive-scale video platform that can handle billions of users and petabytes of content. The design incorporates modern distributed systems principles, microservices architecture, event-driven patterns, and advanced scaling techniques.

The 10x scaling strategy leverages the Scale Cube dimensions, applies CAP theorem principles strategically, and utilizes cutting-edge technologies to ensure the platform remains performant, reliable, and cost-effective as it grows. The architecture is designed to be resilient, observable, and maintainable while providing an excellent user experience globally.
