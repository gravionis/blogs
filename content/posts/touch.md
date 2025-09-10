+++
date = '2024-05-03T12:44:47+10:00'
draft = false
title = 'Senior Developer Interview Questions'
tags = ['Interview', 'Senior']
+++

Each question targets specific competencies: architectural decision-making, operational resilience, performance optimization, security implementation, team coordination and behavioural. The questions are designed to reveal whether you've actually solved these problems in production, not just read about them. The best answers demonstrate practical wisdom gained from building systems that handle millions of requests, managing teams across multiple services, and making architectural decisions under real-world constraints.

## Architecture & Design Patterns (1-20)

1. **How would you handle distributed transactions across multiple microservices without using 2PC?**
   *Probes your knowledge of saga patterns, event sourcing, and eventual consistency. Expect follow-ups about compensation logic and handling partial failures.*

2. **Design a system where Service A needs data from Services B, C, and D, but you can't make synchronous calls due to latency requirements.**
   *Tests understanding of CQRS, event-driven architecture, data replication strategies, and read models. Look for async patterns and data composition techniques.*

3. **How do you prevent cascading failures in a microservices architecture with 50+ services?**
   *Covers circuit breakers, bulkheads, timeouts, rate limiting, graceful degradation, and chaos engineering principles. Expect scenarios about dependency chains.*

4. **You have a microservice that needs to query data spanning 5 different services. How do you handle this without violating service boundaries?**
   *Explores data composition patterns, API gateways, backend for frontend (BFF), and when to denormalize data. Tests service boundary understanding.*

5. **Explain the trade-offs between orchestration vs choreography in microservices. When would you choose each?**
   *Assesses knowledge of workflow patterns, central coordination vs distributed coordination, complexity management, and failure handling strategies.*

6. **How would you design a microservices architecture for a system that needs to process 1 billion events per day with strict ordering requirements?**
   *Tests knowledge of event streaming, partitioning strategies, Kafka/Kinesis, ordering guarantees, and handling hot partitions. Look for discussion of trade-offs between ordering and scalability.*

7. **What's your strategy for handling backward and forward compatibility when multiple versions of services need to coexist?**
   *Probes API versioning strategies, contract testing, schema evolution, feature toggles, and canary deployments. Expect questions about breaking changes and migration strategies.*

8. **How do you implement the Saga pattern for a complex business process spanning 10 microservices with potential rollback scenarios?**
   *Deep dive into compensation logic, saga orchestrator vs choreography, handling partial failures, timeout management, and state machine design.*

9. **Design a distributed cache strategy that maintains consistency across 20 microservices without creating a single point of failure.**
   *Covers cache patterns (write-through, write-behind, cache-aside), invalidation strategies, eventual consistency, Redis clustering, and cache warming.*

10. **How would you implement event sourcing across multiple microservices while ensuring data consistency and auditability?**
    *Tests understanding of event stores, snapshots, replay mechanisms, eventual consistency, CQRS integration, and handling schema changes in events.*

11. **What's your approach to handling shared reference data (like currency codes, country lists) across 100+ microservices?**
    *Explores data replication vs centralization, caching strategies, update propagation, versioning of reference data, and handling stale data scenarios.*

12. **How do you design microservices boundaries when you have complex domain relationships and high cohesion requirements?**
    *Assesses domain-driven design knowledge, bounded contexts, aggregate boundaries, and the tension between service autonomy and data consistency.*

13. **Explain how you'd implement the Bulkhead pattern in a microservices architecture with different SLA requirements per service.**
    *Tests resource isolation strategies, thread pools, connection pools, circuit breakers per dependency, and handling different failure modes.*

14. **How would you handle a scenario where Service A depends on Services B, C, and D, but they have different uptime requirements (99.9% vs 99.99%)?**
    *Covers dependency analysis, graceful degradation, fallback mechanisms, caching strategies, and SLA composition across service chains.*

15. **Design a microservices architecture for a multi-tenant SaaS application with tenant-specific customizations.**
    *Explores tenant isolation strategies, data partitioning, customization without service proliferation, and handling tenant-specific SLAs.*

16. **How do you implement the Strangler Fig pattern when migrating from a monolith with 500+ database tables?**
    *Tests incremental migration strategies, data synchronization during transition, routing strategies, and handling shared data during migration.*

17. **What's your strategy for handling cross-cutting concerns (logging, security, monitoring) without violating microservices principles?**
    *Assesses knowledge of service mesh, sidecars, shared libraries vs duplication, and maintaining service autonomy while ensuring consistency.*

18. **How would you design a system where some microservices need ACID transactions while others can work with eventual consistency?**
    *Explores hybrid architectures, consistency patterns, data flow design, and managing different consistency requirements within one system.*

19. **Explain how you'd implement the Circuit Breaker pattern with different failure thresholds for different types of errors.**
    *Tests understanding of failure classification, adaptive thresholds, half-open state management, and handling transient vs permanent failures.*

20. **How do you handle service discovery and load balancing in a hybrid cloud environment with services across multiple regions?**
    *Covers service mesh, DNS-based discovery, health checks, latency-aware routing, and handling network partitions between regions.*

## Data Management & Persistence (21-40)

21. **How would you migrate from a monolithic database to microservices without downtime and with zero data loss?**
    *Tests knowledge of database decomposition, dual writes, event sourcing, CDC (Change Data Capture), and phased migration strategies. Expect questions about handling referential integrity.*

22. **Design a data synchronization strategy for microservices that need to maintain materialized views of data from other services.**
    *Covers CQRS, event-driven updates, eventual consistency, conflict resolution, and handling out-of-order events. Look for discussion of data freshness requirements.*

23. **How do you implement distributed caching with cache invalidation across microservices without race conditions?**
    *Explores cache coherence protocols, versioning strategies, TTL vs event-based invalidation, and handling cache stampede scenarios.*

24. **What's your approach to handling database schema evolution when multiple microservices share data contracts?**
    *Tests contract-first development, schema registries, backward compatibility, migration strategies, and handling breaking changes in data contracts.*

25. **How would you implement a distributed search capability across data owned by different microservices?**
    *Covers search federation, data indexing strategies, real-time vs batch updates, search result aggregation, and handling service failures during search.*

26. **Design a strategy for handling large file uploads and processing across multiple microservices.**
    *Tests knowledge of chunked uploads, async processing, event-driven workflows, storage strategies, and handling partial upload failures.*

27. **How do you maintain referential integrity across microservices without distributed transactions?**
    *Explores eventual consistency patterns, compensating actions, data validation strategies, and handling orphaned references.*

28. **What's your approach to implementing read replicas and write masters across geographically distributed microservices?**
    *Covers data replication patterns, read-write splitting, handling replication lag, conflict resolution, and geo-sharding strategies.*

29. **How would you handle data archiving and retention policies across 50+ microservices with different compliance requirements?**
    *Tests understanding of data lifecycle management, GDPR compliance, automated archiving, cross-service data relationships, and audit trails.*

30. **Design a solution for real-time data synchronization between microservices and a data warehouse.**
    *Covers CDC, event streaming, ETL vs ELT patterns, handling schema drift, and maintaining data quality during real-time ingestion.*

31. **How do you implement optimistic locking across distributed microservices to prevent data conflicts?**
    *Tests understanding of version vectors, ETags, conditional updates, conflict detection and resolution, and handling concurrent modifications.*

32. **What's your strategy for handling batch processing jobs that need data from multiple microservices?**
    *Covers batch orchestration patterns, data extraction strategies, handling partial failures, job scheduling, and maintaining data consistency.*

33. **How would you design a microservices architecture for a system with complex reporting requirements across multiple data domains?**
    *Explores CQRS with read models, data denormalization strategies, reporting databases, real-time vs batch reporting, and handling data joins.*

34. **Explain your approach to handling database connection pooling and management across 100+ microservice instances.**
    *Tests knowledge of connection pool sizing, connection sharing strategies, database proxy patterns, and handling connection exhaustion.*

35. **How do you implement data lineage tracking across microservices for compliance and auditing?**
    *Covers event sourcing, audit trails, data provenance tracking, cross-service correlation, and handling data transformation chains.*

36. **What's your strategy for handling temporal data and time-based queries across distributed microservices?**
    *Tests understanding of event time vs processing time, handling clock skew, temporal consistency, and distributed timestamp ordering.*

37. **How would you design a backup and disaster recovery strategy for microservices with different RTO/RPO requirements?**
    *Covers backup strategies, cross-region replication, service dependency mapping, recovery orchestration, and testing disaster scenarios.*

38. **Explain how you'd handle data migration between different database technologies while services are running.**
    *Tests dual-write patterns, data validation strategies, rollback mechanisms, and handling migration failures without downtime.*

39. **How do you implement distributed locks for resources that span multiple microservices?**
    *Covers distributed locking algorithms, lease-based locks, handling lock timeouts, deadlock prevention, and lock granularity strategies.*

40. **What's your approach to handling data consistency during blue-green deployments of data-dependent services?**
    *Tests understanding of deployment patterns with stateful services, data migration coordination, and handling schema changes during deployments.*

## Communication & Integration (41-60)

41. **How would you design an API gateway that can handle 100K requests per second with sub-50ms latency?**
    *Tests knowledge of load balancing algorithms, connection pooling, caching strategies, request routing optimization, and performance bottleneck identification.*

42. **What's your strategy for handling API versioning across 200+ microservices with different release cycles?**
    *Covers semantic versioning, contract evolution, sunset policies, version negotiation, and coordinating breaking changes across teams.*

43. **How do you implement reliable message delivery in an event-driven architecture with exactly-once semantics?**
    *Tests understanding of message deduplication, idempotency keys, distributed consensus, outbox pattern, and handling duplicate message scenarios.*

44. **Design a solution for handling long-running workflows that span multiple microservices over days or weeks.**
    *Covers workflow orchestration patterns, state persistence, timeout handling, human task integration, and resuming interrupted workflows.*

45. **How would you implement request correlation and distributed tracing across async message chains?**
    *Tests trace context propagation, correlation ID generation, handling message splits/merges, and maintaining trace continuity across async boundaries.*

46. **What's your approach to handling service mesh configuration for 500+ microservice instances?**
    *Covers service mesh architecture, policy management, traffic routing rules, security policies, and handling configuration drift at scale.*

47. **How do you design GraphQL federation across microservices while maintaining service autonomy?**
    *Tests schema stitching vs federation, resolver performance, N+1 query problems, schema evolution, and handling service dependencies.*

48. **Explain how you'd implement rate limiting and throttling across different service tiers and priorities.**
    *Covers rate limiting algorithms, distributed rate limiting, priority queuing, backpressure mechanisms, and handling burst traffic.*

49. **How would you handle webhook delivery and retry logic across multiple external systems?**
    *Tests retry strategies, exponential backoff, dead letter queues, webhook security, and handling webhook failures and timeouts.*

50. **What's your strategy for implementing idempotency across RESTful APIs in a distributed system?**
    *Covers idempotency keys, operation deduplication, state management, handling concurrent requests, and designing idempotent operations.*

51. **How do you design async communication patterns for microservices with different message ordering requirements?**
    *Tests understanding of message queues, topic partitioning, ordering guarantees, handling out-of-order messages, and partial ordering strategies.*

52. **Explain your approach to handling protocol translation (REST to gRPC to message queues) in microservices.**
    *Covers protocol bridges, message transformation, handling different serialization formats, and maintaining semantic consistency across protocols.*

53. **How would you implement content-based routing in a microservices architecture with complex business rules?**
    *Tests message routing patterns, rule engines, dynamic routing, A/B testing integration, and handling routing rule changes without downtime.*

54. **What's your strategy for handling service-to-service authentication and authorization at scale?**
    *Covers JWT tokens, OAuth2, mTLS, service mesh security, token refresh strategies, and handling compromised credentials.*

55. **How do you design event streaming architecture for microservices with different event retention needs?**
    *Tests knowledge of event stores, compaction strategies, archival policies, event replay capabilities, and handling storage costs.*

56. **Explain how you'd handle API deprecation across dependent services without breaking functionality.**
    *Covers deprecation timelines, migration strategies, feature toggles, graceful degradation, and coordinating changes across teams.*

57. **How would you implement message deduplication in a high-throughput event-driven system?**
    *Tests deduplication algorithms, bloom filters, sliding window techniques, distributed deduplication, and handling memory constraints.*

58. **What's your approach to handling partial failures in request/response chains spanning 10+ services?**
    *Covers timeout strategies, circuit breakers, fallback mechanisms, partial response handling, and maintaining user experience during failures.*

59. **How do you design pub/sub patterns for microservices with different consistency and durability requirements?**
    *Tests understanding of message brokers, persistence levels, acknowledgment strategies, and handling subscriber failures.*

60. **Explain your strategy for handling service contracts and schema evolution in event-driven architectures.**
    *Covers schema registries, compatibility checking, event versioning, contract testing, and handling breaking changes in event schemas.*

## Observability & Monitoring (61-75)

61. **A user request is failing somewhere in a chain of 12 microservices. Walk me through your debugging approach.**
    *Assesses distributed tracing, correlation IDs, structured logging, debugging strategies in distributed systems, and systematic troubleshooting methodology.*

62. **How do you implement distributed tracing with sampling strategies that don't impact performance?**
    *Tests knowledge of trace sampling algorithms, adaptive sampling, trace storage optimization, and balancing observability with performance.*

63. **What's your strategy for implementing effective alerting that reduces noise but catches real issues?**
    *Covers alert fatigue, SLI/SLO-based alerting, anomaly detection, alert correlation, and implementing smart alerting thresholds.*

64. **How would you design logging architecture for microservices generating 10TB of logs per day?**
    *Tests log aggregation, storage optimization, log retention policies, cost management, and structured logging strategies at scale.*

65. **Explain how you'd implement SLI/SLO monitoring across microservices with cascading dependencies.**
    *Covers error budgets, dependency mapping, composite SLIs, blame-free postmortems, and handling SLO violations in dependency chains.*

66. **How do you design metrics collection and aggregation for microservices without creating performance bottlenecks?**
    *Tests metric aggregation patterns, push vs pull models, metric cardinality management, and handling high-frequency metrics.*

67. **What's your approach to implementing chaos engineering in production microservices?**
    *Covers chaos experiments, blast radius control, automated failure injection, measuring system resilience, and building confidence through controlled failures.*

68. **How would you handle log correlation across async workflows spanning multiple services and time zones?**
    *Tests correlation strategies across async boundaries, handling clock skew, trace reconstruction, and maintaining context across time zones.*

69. **Explain your strategy for implementing cost monitoring and optimization across cloud-native microservices.**
    *Covers cost attribution, resource optimization, rightsizing, waste identification, and implementing cost-aware architectures.*

70. **How do you design health checks for microservices with complex dependency chains?**
    *Tests health check patterns, dependency health aggregation, avoiding cascading health failures, and implementing meaningful readiness checks.*

71. **What's your approach to implementing distributed profiling across microservices for performance optimization?**
    *Covers continuous profiling, distributed flame graphs, performance hotspot identification, and profiling without performance impact.*

72. **How would you handle security monitoring and threat detection across microservices architecture?**
    *Tests security observability, anomaly detection, intrusion detection, audit logging, and implementing security dashboards.*

73. **Explain how you'd implement business metrics monitoring alongside technical metrics in microservices.**
    *Covers business KPI tracking, real-time business dashboards, correlating business and technical metrics, and measuring business impact.*

74. **How do you design dashboard and visualization strategies for operations teams managing 200+ services?**
    *Tests information hierarchy, dashboard design principles, role-based views, alert visualization, and reducing cognitive load.*

75. **What's your strategy for implementing automated incident response in microservices environments?**
    *Covers automated remediation, runbook automation, escalation policies, incident correlation, and self-healing systems.*

## Performance & Scalability (76-85)

76. **Service A calls Service B 10,000 times per request. How do you optimize this anti-pattern?**
    *Tests batching strategies, caching, async processing, and recognizing anti-patterns in service communication. Look for N+1 query solutions.*

77. **Design a microservices architecture that can handle 10x traffic spikes in under 30 seconds.**
    *Explores auto-scaling, load balancing, circuit breakers, capacity planning, warm-up strategies, and handling cold start problems.*

78. **How would you implement auto-scaling for microservices with different resource requirements and scaling patterns?**
    *Covers horizontal vs vertical scaling, predictive scaling, custom metrics, scaling policies, and handling stateful services.*

79. **What's your strategy for handling database connection limits when scaling microservices horizontally?**
    *Tests connection pooling, database proxies, read replicas, connection sharing strategies, and database scaling patterns.*

80. **How do you design caching strategies for microservices to achieve sub-10ms response times?**
    *Covers multi-level caching, cache warming, cache coherence, edge caching, and optimizing cache hit rates.*

81. **Explain how you'd optimize network communication between microservices in high-latency environments.**
    *Tests connection reuse, protocol optimization, data compression, regional deployment, and minimizing network round trips.*

82. **How would you handle memory management and garbage collection across JVM-based microservices at scale?**
    *Covers GC tuning, memory profiling, heap sizing, off-heap storage, and handling GC pauses in distributed systems.*

83. **What's your approach to implementing connection pooling and resource management across distributed services?**
    *Tests connection pool sizing, resource sharing, connection lifecycle management, and handling resource exhaustion.*

84. **How do you design load balancing strategies for microservices with different computational requirements?**
    *Covers load balancing algorithms, weighted routing, sticky sessions, health-aware routing, and handling heterogeneous workloads.*

85. **Explain your strategy for optimizing cold start times in serverless microservices architectures.**
    *Tests provisioned concurrency, container optimization, dependency initialization, warm-up strategies, and JIT compilation optimization.*

## Security & Compliance (86-95)

86. **How do you implement zero-trust security architecture across microservices in multi-cloud environments?**
    *Tests service mesh security, mTLS implementation, identity verification at every hop, network segmentation, and cross-cloud security policies.*

87. **What's your strategy for handling secrets management and rotation across 300+ microservice instances?**
    *Covers secret rotation automation, vault integration, secret injection patterns, handling rotation failures, and minimizing secret exposure.*

88. **How would you implement end-to-end encryption for data flowing through multiple microservices?**
    *Tests encryption key management, envelope encryption, handling encrypted data processing, key rotation, and performance implications.*

89. **Explain your approach to implementing GDPR compliance (data deletion, portability) across distributed microservices.**
    *Covers data discovery, deletion orchestration, data export coordination, consent management, and handling data in event streams.*

90. **How do you design audit logging and compliance reporting for microservices handling sensitive data?**
    *Tests tamper-proof logging, log integrity, compliance automation, audit trail correlation, and handling audit log storage at scale.*

91. **What's your strategy for implementing network segmentation and security policies in microservices?**
    *Covers microsegmentation, service mesh policies, network policies, traffic inspection, and implementing least-privilege networking.*

92. **How would you handle security vulnerability scanning and patching across containerized microservices?**
    *Tests container scanning, vulnerability management, automated patching, handling zero-day vulnerabilities, and coordinating security updates.*

93. **Explain your approach to implementing identity and access management across service boundaries.**
    *Covers JWT propagation, token validation, service identity, RBAC implementation, and handling identity federation.*

94. **How do you design threat modeling and security assessment for evolving microservices architectures?**
    *Tests continuous threat modeling, attack surface analysis, security testing integration, and adapting security to architectural changes.*

95. **What's your strategy for handling security incident response across distributed microservices?**
    *Covers incident containment, forensic data collection, impact analysis, coordinated response, and post-incident security hardening.*

## DevOps & Operations (96-100)

96. **A critical bug needs to be fixed across 15 microservices. Describe your deployment strategy.**
    *Tests coordinated deployment strategies, dependency ordering, rollback planning, feature toggles, and minimizing blast radius. Expect questions about handling deployment failures mid-process.*

97. **How would you implement infrastructure as code for microservices across multiple cloud providers?**
    *Covers Terraform/Pulumi patterns, environment parity, multi-cloud abstractions, state management, and handling cloud-specific services. Look for discussion of vendor lock-in mitigation.*

98. **What's your strategy for handling database migrations across microservices during zero-downtime deployments?**
    *Tests backward-compatible schema changes, migration coordination, data migration patterns, handling migration failures, and maintaining data consistency during deployments.*

99. **How do you design CI/CD pipelines for microservices with complex interdependencies and testing requirements?**
    *Covers pipeline orchestration, dependency testing, contract testing, integration test strategies, and handling flaky tests. Expect questions about testing pyramid in distributed systems.*

100. **Explain your approach to capacity planning and resource allocation for a growing microservices architecture.**
     *Tests performance modeling, resource forecasting, cost optimization, rightsizing strategies, and handling unpredictable growth patterns. Look for discussion of monitoring-driven capacity decisions.*


## Amazon Leadership Principles - Behavioral Questions

### 1. Customer Obsession

- Tell me about a time when protecting customer experience directly caused a significant financial or reputational loss for your business. What did you do, and would you do it again?

- Describe a time you knowingly introduced short-term customer pain for a long-term benefit. How did you justify it?

### 2. Ownership

- Share an example where something failed spectacularly in your absence. What processes or ownership gaps did you miss?

- Tell me about a time when you took ownership for a failure that you didn't cause. Why, and what happened after?

### 3. Invent and Simplify

- Describe a time when your "simplification" broke an existing complex but working system. How did you recover?

- Tell me about a radical idea you killed despite believing in it deeply. Why did you abandon it?

### 4. Are Right, A Lot

- Share an instance where being right made you unpopular or politically isolated. How did you navigate that?

- Tell me about a time when you bet your reputation on a decision that turned out wrong. What did you do next?

### 5. Learn and Be Curious

- Describe a time when your lack of curiosity led to a major miss or blind spot. How did you correct it?

- What's the most uncomfortable truth you uncovered by asking "why" too many times?

### 6. Hire and Develop the Best

- Share an example of when you hired or promoted the wrong person. What damage did it cause and what did you learn?

- Tell me about a time when you had to let go of a high performer who was toxic to the culture. How did you balance results vs. culture?

### 7. Insist on the Highest Standards

- Tell me about a time when raising the bar damaged relationships with peers or leadership. Was it worth it?

- Describe when enforcing high standards led to project delays or cost overruns. How did you defend that?

### 8. Think Big

- Share a time when your big vision failed so badly that people lost confidence in your judgment. How did you rebuild trust?

- Tell me about a time when thinking too big blinded you to an obvious simpler path.

### 9. Bias for Action

- Describe a high-stakes decision you made in minutes that caused lasting consequences. How did you recover?

- Tell me about a time when moving too fast destroyed alignment with key stakeholders.

### 10. Frugality

- Share an example where cost-cutting compromised customer trust or team morale. How did you justify it?

- Tell me about a time you turned down extra resources and regretted it.

### 11. Earn Trust

- Describe the hardest moment of rebuilding trust when you were seen as dishonest or incompetent. What did you do over months or years?

- Tell me about a time when being radically transparent damaged your credibility in the short term.

### 12. Dive Deep

- Share an example where your deep dive uncovered uncomfortable truths that leadership didn't want to hear. What did you do?

- Tell me about a time when diving deep caused you to lose sight of the bigger picture.

### 13. Have Backbone; Disagree and Commit

- Describe the most controversial stand you ever took that risked your job, promotion, or reputation. What happened?

- Tell me about a time you disagreed with a decision, lost, but secretly believed it would fail — and it did. How did you react?

### 14. Deliver Results

- Share a story where you sacrificed relationships, personal well-being, or long-term strategy just to deliver results. Would you repeat that choice?

- Tell me about a time when you failed to deliver despite doing everything "right." How did you explain that?

### 15. Strive to be Earth's Best Employer

- Describe when advocating for employee well-being made you look weak or unaligned with business goals. What was the fallout?

- Tell me about a time you failed to protect a team member from burnout or unfair treatment.

### 16. Success and Scale Bring Broad Responsibility

- Share an example where scaling your product or system harmed society, the environment, or customers in an unexpected way. What role did you play in fixing it?

- Tell me about the hardest ethical decision you made when balancing business success with broader responsibility.

---

*These questions are designed to probe for real experiences where candidates faced difficult trade-offs, failures, or complex ethical decisions. They go beyond surface-level accomplishments to understand how someone handles adversity, learns from mistakes, and navigates competing priorities.*
