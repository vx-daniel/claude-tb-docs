# ThingsBoard Platform Documentation

Technical documentation for the ThingsBoard IoT platform, prepared for platform rewrite.

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

- [System Overview](./01-architecture/system-overview.md) - Component diagram and connections
- Data Flow Overview - End-to-end data paths
- Multi-Tenancy - Tenant isolation model
- Microservices - MSA deployment topology

### [02 - Core Concepts](./02-core-concepts/)
Fundamental entities and data models.

**Entities:**
- [Device](./02-core-concepts/entities/device.md) - IoT devices and their lifecycle
- Asset - Logical groupings and hierarchies
- Tenant - Organization isolation
- Customer - End-user management
- Dashboard - Visualization containers
- Alarm - Alert lifecycle

**Data Model:**
- [Telemetry](./02-core-concepts/data-model/telemetry.md) - Time-series sensor data
- Attributes - Device configuration and state
- RPC - Remote procedure calls

**Identity:**
- Entity IDs - UUID-based identification
- Credentials - Authentication mechanisms

### [03 - Actor System](./03-actor-system/)
Concurrent processing architecture using the actor model.

- [Overview](./03-actor-system/README.md) - Why actors, hierarchy, message routing
- Actor Types - Tenant, Device, RuleChain actors
- Message Types - Internal message taxonomy
- Lifecycle - Creation, processing, destruction

### [04 - Rule Engine](./04-rule-engine/)
Configurable data processing pipelines.

- Rule Chain Structure - How chains are composed
- Message Flow - TbMsg routing through nodes
- Node Categories - Filter, Transform, Action, External
- Node Development - Creating custom nodes

### [05 - Transport Layer](./05-transport-layer/)
Device communication protocols.

- Transport Contract - Common interface
- MQTT - Primary IoT protocol
- CoAP - Constrained devices
- HTTP - REST-based communication
- LwM2M - Device management protocol
- SNMP - Network monitoring

### [06 - API Layer](./06-api-layer/)
External interfaces for users and integrations.

- REST API - CRUD operations, conventions
- WebSocket - Real-time subscriptions
- Authentication - JWT and session management

### [07 - Data Persistence](./07-data-persistence/)
Storage patterns and database architecture.

- Database Schema - Entity storage
- Time-Series Storage - Telemetry persistence
- Caching Strategy - Performance optimization

### [08 - Message Queue](./08-message-queue/)
Inter-service communication.

- Queue Architecture - Topic structure
- Partitioning - Load distribution
- Message Formats - Serialization

### [09 - Security](./09-security/)
Authentication, authorization, and isolation.

- Authentication - Login mechanisms
- Authorization - Permission model
- Tenant Isolation - Data separation

### [10 - Frontend](./10-frontend/)
Web UI architecture.

- Module Structure - Component organization
- State Management - Data flow patterns
- Widget System - Extensible visualizations

### [11 - Microservices](./11-microservices/)
Service decomposition and responsibilities.

- Core Node - Main application service
- Transport Services - Protocol handlers
- JS Executor - Script execution
- Web UI - Frontend serving

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
