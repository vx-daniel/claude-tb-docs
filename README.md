# ThingsBoard Platform Documentation

Technical documentation for the ThingsBoard IoT platform, prepared for platform rewrite.

> **Progress**: See [ROADMAP.md](./ROADMAP.md) for documentation status and next steps.

## Purpose

This documentation captures the behavior, architecture, and data flows of the ThingsBoard platform in technology-agnostic terms. It serves as a reference for understanding the existing system before implementing a rewrite.

## Quick Start

If you're new to this codebase, read these documents in order:

1. [Glossary](./GLOSSARY.md) - Learn the terminology
2. [System Overview](./01-architecture/system-overview.md) - Understand the big picture
3. [Device Entity](./02-core-concepts/entities/device.md) - The central IoT concept
4. [Actor System](./03-actor-system/README.md) - How the runtime works
5. [Telemetry](./02-core-concepts/data-model/telemetry.md) - Primary data type

## Documentation Structure

### [01 - Architecture](./01-architecture/)
High-level system design, component relationships, and deployment topologies.

- [System Overview](./01-architecture/system-overview.md) - Component diagram, technology stack, and connections
- [Multi-Tenancy](./01-architecture/multi-tenancy.md) - Tenant isolation model and data separation

### [02 - Core Concepts](./02-core-concepts/)
Fundamental entities and data models.

**Entities:**
- [Entity Types Overview](./02-core-concepts/entities/entity-types-overview.md) - All 27 entity types
- [Device](./02-core-concepts/entities/device.md) - IoT devices and their lifecycle

**Data Model:**
- [Telemetry](./02-core-concepts/data-model/telemetry.md) - Time-series sensor data
- [Attributes](./02-core-concepts/data-model/attributes.md) - Device configuration and state
- [Calculated Fields](./02-core-concepts/data-model/calculated-fields.md) - Computed values (v4.x feature)

### [03 - Actor System](./03-actor-system/)
Concurrent processing architecture using the actor model.

- [Overview](./03-actor-system/README.md) - Why actors, hierarchy, TbActorSystem, message routing

### [04 - Rule Engine](./04-rule-engine/)
Configurable data processing pipelines.

- [Overview](./04-rule-engine/README.md) - Rule engine architecture, 60+ built-in nodes
- [Rule Chain Structure](./04-rule-engine/rule-chain-structure.md) - How chains are composed
- [Message Flow](./04-rule-engine/message-flow.md) - TbMsg routing through nodes
- [Node Categories](./04-rule-engine/node-categories.md) - Filter, Transform, Action, External nodes
- [Node Development Contract](./04-rule-engine/node-development-contract.md) - Creating custom nodes

### [05 - Transport Layer](./05-transport-layer/)
Device communication protocols.

- [Transport Contract](./05-transport-layer/transport-contract.md) - Common interface for all transports
- [MQTT](./05-transport-layer/mqtt.md) - Primary IoT protocol
- [HTTP](./05-transport-layer/http.md) - REST-based communication
- [CoAP](./05-transport-layer/coap.md) - Constrained devices protocol
- [LwM2M](./05-transport-layer/lwm2m.md) - Device management protocol
- [SNMP](./05-transport-layer/snmp.md) - Network monitoring protocol

### [06 - API Layer](./06-api-layer/)
External interfaces for users and integrations.

- [REST API Overview](./06-api-layer/rest-api-overview.md) - 57 controllers, CRUD operations, conventions
- [Authentication](./06-api-layer/authentication.md) - JWT, OAuth2, API Keys, 2FA
- [Device API](./06-api-layer/device-api.md) - Device-specific endpoints
- [WebSocket Overview](./06-api-layer/websocket-overview.md) - Real-time connections
- [Subscription Model](./06-api-layer/subscription-model.md) - Data subscription patterns

### [07 - Data Persistence](./07-data-persistence/)
Storage patterns and database architecture.

- [Database Schema](./07-data-persistence/database-schema.md) - Entity storage, caching strategies
- [Time-Series Storage](./07-data-persistence/timeseries-storage.md) - Telemetry persistence, partitioning

### [08 - Message Queue](./08-message-queue/)
Inter-service communication.

- [Queue Architecture](./08-message-queue/queue-architecture.md) - Kafka, topic structure, factories
- [Partitioning](./08-message-queue/partitioning.md) - Hash-based distribution, tenant isolation

### [10 - Frontend](./10-frontend/)
Web UI architecture (Angular 18.2.13).

- [Angular Architecture](./10-frontend/angular-architecture.md) - Module structure, NgRx state management
- [Widget System](./10-frontend/widget-system.md) - Extensible visualizations, 40+ context services

### [11 - Microservices](./11-microservices/)
Service decomposition and deployment.

- [Overview](./11-microservices/README.md) - Service types, Zookeeper discovery, HAProxy load balancing

## Technology Stack (v4.3.0-RC)

| Layer | Technology |
|-------|------------|
| Runtime | Java 17, Spring Boot 3.4.10 |
| Message Queue | Kafka 3.9.1 |
| Databases | PostgreSQL, Cassandra, TimescaleDB |
| Cache | Redis/Valkey, Caffeine |
| Frontend | Angular 18.2.13, NgRx, Material Design |
| Service Discovery | Apache Zookeeper |
| Load Balancer | HAProxy |

## Conventions

### Diagrams
All architecture and flow diagrams use [Mermaid](https://mermaid.js.org/) syntax for version control compatibility.

### Technology-Agnostic Language
Documentation describes **behaviors and contracts**, not implementation details:
- "message handler" not "Spring Bean"
- "persistent storage" not "JPA Repository"
- "scheduled task" not "Quartz Job"

### Cross-References
Documents link to related topics. Use the "See Also" section at the bottom of each document.

## Source Reference

This documentation is derived from the ThingsBoard source code at:
```
~/work/viaanix/thingsboard/
```

Version: 4.3.0-RC

## Document Statistics

| Category | Documents |
|----------|-----------|
| Architecture | 2 |
| Core Concepts | 5 |
| Actor System | 1 |
| Rule Engine | 5 |
| Transport Layer | 6 |
| API Layer | 5 |
| Data Persistence | 2 |
| Message Queue | 2 |
| Frontend | 2 |
| Microservices | 1 |
| **Total** | **31** |
