+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = 'Microservice Design Patterns'
tags = ['Event Driven Architecture', 'Microservices', 'Interview']
+++

In this post, we explore Microservice Design Patterns, focusing on decomposition, communication, resilience, data consistency, observability, and security. Learn strategies to build scalable, efficient, and maintainable distributed systems aligned with modern software principles.

## Hexagonal Architecture

Hexagonal architecture is a design pattern that addresses key challenges in software design. Here are its main points:
![hexagonal](../hexagonal.png)
- **Encapsulation of Domain Logic**: Keeps the domain logic isolated and independent of external systems.
- **Adapters and Ports**: 
  - Adapters expose the domain while keeping it encapsulated.
  - Ports abstract business logic from protocols, enabling loose coupling.
- **Context Boundaries**: Ensures entities are centralized and context boundaries are well-defined.
- **Domain-Driven Design (DDD)**: Aligns with DDD principles by focusing on the core domain and its logic.
- **Flexibility and Scalability**: Promotes flexibility and scalability by decoupling components.
- **Enables Patterns**: Supports patterns like transactional messaging (e.g., polling publishers).
- **Maintainability**: Simplifies maintenance by separating concerns and reducing dependencies.
## Pattern Language
![](../pattern_language.png)

## Architecture & Decomposition Patterns

### Strangler Application
- A pattern for incrementally migrating a monolithic application to a microservices architecture.

### Monolithic Architecture
- A single, unified codebase where all components are tightly coupled.

### Microservice Architecture
- A distributed system where each service is independently deployable and focused on a specific business capability.

### Decompose by Business Capability
- Break down the system into services aligned with business capabilities.

### Decompose by Subdomain
- Decompose the system based on subdomains identified in domain-driven design.

## Inter-Service Communication Patterns

### Communication Style
- Defines how services interact with each other.

### Remote Procedure Invocation (RPI)
- A synchronous communication style where one service calls another directly.

### Messaging
- An asynchronous communication style using message brokers.

### Service Discovery
- Mechanisms for services to find each other dynamically.
  - Self-Registration
  - Client-Side Discovery
  - 3rd-Party Registration
  - Server-Side Discovery

## Resilience (Reliability)

### Circuit Breaker
- A pattern to prevent cascading failures by stopping requests to a failing service.

### Transactional Messaging
- Ensures reliable message delivery in distributed systems.
  - Transactional Outbox
  - Polling Publisher
  - Transaction Log Tailing

## Data Consistency Patterns

### Saga
- A pattern for managing distributed transactions using a sequence of local transactions.

## Business Logic Patterns

### Transaction Script
- A procedural approach to implementing business logic.

### Domain Model
- An object-oriented approach to encapsulating business logic.

### Aggregate
- A cluster of domain objects treated as a single unit.

## Event-Driven Patterns

### Event Sourcing
- A pattern where state changes are captured as a sequence of events.

## Data Query Patterns

### API Composition
- A pattern for aggregating data from multiple services into a single API response.

### Command Query Responsibility Segregation (CQRS)
- A pattern that separates read and write operations into different models.

## External API Patterns

### API Gateway
- A single entry point for managing external API requests.

### Backends for Frontends (BFF)
- A pattern where each frontend has a dedicated backend service.

## Security Patterns

### Access Token
- A mechanism for authenticating and authorizing API requests.

## Operational / Observability Patterns

### Externalized Configuration
- A pattern for managing configuration outside the application code.

### Health Check API
- An API endpoint for monitoring the health of a service.

### Log Aggregation
- A pattern for centralizing and analyzing logs from multiple services.

## Testing Patterns

### Consumer-Driven Contract Test
- A testing approach where consumers define the contract.

### Consumer-Side Contract Test
- A testing approach where the consumer verifies the provider's contract.

## Deployment Patterns

### Sidecar
- A pattern for deploying auxiliary components alongside the main service.
