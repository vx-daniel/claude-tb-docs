# Documentation Roadmap

This file tracks documentation progress for the ThingsBoard platform rewrite preparation.

**Last Updated**: 2026-01-10

## Progress Summary

| Phase | Status | Documents | Completed |
|-------|--------|-----------|-----------|
| Phase 1: Foundation | ✅ Complete | 6 | 6 |
| Phase 2: Data Pathways | ✅ Complete | 5 | 5 |
| Phase 3: Rule Engine | ✅ Complete | 5 | 5 |
| Phase 4: API Surface | ✅ Complete | 5 | 5 |
| Phase 5: Persistence & Infrastructure | ✅ Complete | 5 | 5 |
| Phase 6: Frontend & Remaining | ✅ Complete | 6 | 6 |

**Total Progress**: 32 / 32 core documents (100%)

---

## Phase 1: Foundation ✅

Establishes the mental model for understanding the platform.

| Document | Status | Path |
|----------|--------|------|
| Project README | ✅ Done | `README.md` |
| Glossary | ✅ Done | `GLOSSARY.md` |
| System Overview | ✅ Done | `01-architecture/system-overview.md` |
| Device Entity | ✅ Done | `02-core-concepts/entities/device.md` |
| Actor System Overview | ✅ Done | `03-actor-system/README.md` |
| Telemetry Data Model | ✅ Done | `02-core-concepts/data-model/telemetry.md` |

---

## Phase 2: Data Pathways ✅

How data moves through the system.

| Document | Status | Path | Priority |
|----------|--------|------|----------|
| Telemetry Data Model | ✅ Done | `02-core-concepts/data-model/telemetry.md` | 1 |
| Attributes Data Model | ✅ Done | `02-core-concepts/data-model/attributes.md` | 2 |
| Transport Contract | ✅ Done | `05-transport-layer/transport-contract.md` | 3 |
| MQTT Protocol | ✅ Done | `05-transport-layer/mqtt.md` | 4 |
| Message Queue Architecture | ✅ Done | `08-message-queue/queue-architecture.md` | 5 |

---

## Phase 3: Rule Engine ✅

The "business logic" layer - configurable data processing.

| Document | Status | Path | Priority |
|----------|--------|------|----------|
| Rule Engine Overview | ✅ Done | `04-rule-engine/README.md` | 1 |
| Rule Chain Structure | ✅ Done | `04-rule-engine/rule-chain-structure.md` | 2 |
| Message Flow (TbMsg) | ✅ Done | `04-rule-engine/message-flow.md` | 3 |
| Node Categories | ✅ Done | `04-rule-engine/node-categories.md` | 4 |
| Node Development Contract | ✅ Done | `04-rule-engine/node-development-contract.md` | 5 |

---

## Phase 4: API Surface ✅

External interfaces for users and integrations.

| Document | Status | Path | Priority |
|----------|--------|------|----------|
| REST API Overview | ✅ Done | `06-api-layer/rest-api-overview.md` | 1 |
| Authentication (JWT) | ✅ Done | `06-api-layer/authentication.md` | 2 |
| Device API | ✅ Done | `06-api-layer/device-api.md` | 3 |
| WebSocket Overview | ✅ Done | `06-api-layer/websocket-overview.md` | 4 |
| Subscription Model | ✅ Done | `06-api-layer/subscription-model.md` | 5 |

---

## Phase 5: Persistence & Infrastructure ✅

Storage and deployment patterns.

| Document | Status | Path | Priority |
|----------|--------|------|----------|
| Database Schema | ✅ Done | `07-data-persistence/database-schema.md` | 1 |
| Time-Series Storage | ✅ Done | `07-data-persistence/timeseries-storage.md` | 2 |
| Multi-Tenancy | ✅ Done | `01-architecture/multi-tenancy.md` | 3 |
| Microservices | ✅ Done | `11-microservices/README.md` | 4 |
| Queue Partitioning | ✅ Done | `08-message-queue/partitioning.md` | 5 |

---

## Phase 6: Frontend & Remaining ✅

UI architecture and remaining transports/entities.

| Document | Status | Path | Priority |
|----------|--------|------|----------|
| Angular Architecture | ✅ Done | `10-frontend/angular-architecture.md` | 1 |
| Widget System | ✅ Done | `10-frontend/widget-system.md` | 2 |
| CoAP Protocol | ✅ Done | `05-transport-layer/coap.md` | 3 |
| HTTP Protocol | ✅ Done | `05-transport-layer/http.md` | 4 |
| LwM2M Protocol | ✅ Done | `05-transport-layer/lwm2m.md` | 5 |
| SNMP Protocol | ✅ Done | `05-transport-layer/snmp.md` | 6 |

---

## Additional Documents (As Needed)

### Core Concepts - Entities
| Document | Status | Path |
|----------|--------|------|
| Entity Types Overview | ✅ Done | `02-core-concepts/entities/entity-types-overview.md` |
| Asset Entity | ✅ Done | `02-core-concepts/entities/asset.md` |
| Tenant Entity | ✅ Done | `02-core-concepts/entities/tenant.md` |
| Customer Entity | ✅ Done | `02-core-concepts/entities/customer.md` |
| Dashboard Entity | ✅ Done | `02-core-concepts/entities/dashboard.md` |
| Alarm Entity | ✅ Done | `02-core-concepts/entities/alarm.md` |
| Entity Relations | ⏳ Pending | `02-core-concepts/entities/relations.md` |

### Core Concepts - Data Model
| Document | Status | Path |
|----------|--------|------|
| Calculated Fields | ✅ Done | `02-core-concepts/data-model/calculated-fields.md` |
| RPC (Remote Procedure Call) | ⏳ Pending | `02-core-concepts/data-model/rpc.md` |
| Entity IDs | ⏳ Pending | `02-core-concepts/identity/entity-ids.md` |

### Actor System
| Document | Status | Path |
|----------|--------|------|
| Message Types Reference | ⏳ Pending | `03-actor-system/message-types.md` |
| Device Actor | ⏳ Pending | `03-actor-system/device-actor.md` |
| Rule Chain Actor | ⏳ Pending | `03-actor-system/rule-chain-actor.md` |

### Security
| Document | Status | Path |
|----------|--------|------|
| Authentication | ⏳ Pending | `09-security/authentication.md` |
| Authorization | ⏳ Pending | `09-security/authorization.md` |
| Tenant Isolation | ⏳ Pending | `09-security/tenant-isolation.md` |

### Microservices
| Document | Status | Path |
|----------|--------|------|
| TB Node | ⏳ Pending | `11-microservices/tb-node.md` |
| JS Executor | ⏳ Pending | `11-microservices/js-executor.md` |
| Transport Services | ⏳ Pending | `11-microservices/transport-services.md` |

---

## Key Mermaid Diagrams Needed

### Completed ✅
- [x] System Overview - Component diagram
- [x] Data Flow Overview - End-to-end telemetry
- [x] Actor Hierarchy - Actor tree structure
- [x] Device Lifecycle - State machine
- [x] Device Authentication Flow - Sequence
- [x] Gateway Protocol Flow
- [x] Telemetry Ingestion Flow - Sequence
- [x] Storage Architecture - Dual storage pattern
- [x] WebSocket Subscription Flow

### Pending ⏳
- [x] Microservices Topology
- [x] Multi-Tenant Isolation
- [x] Rule Chain Processing Flow
- [x] MQTT Connect Sequence
- [x] JWT Authentication Sequence
- [x] Alarm Lifecycle Flow
- [x] Database Schema ER Diagram
- [x] Queue Topic Structure
- [x] Frontend Module Dependencies

---

## Source Files Reference

Key ThingsBoard source files for documentation:

| Topic | Source Path |
|-------|-------------|
| Actor System | `application/src/main/java/org/thingsboard/server/actors/` |
| Message Format | `common/message/src/main/java/org/thingsboard/server/common/msg/TbMsg.java` |
| Message Types | `common/data/src/main/java/org/thingsboard/server/common/data/msg/TbMsgType.java` |
| Device Entity | `common/data/src/main/java/org/thingsboard/server/common/data/Device.java` |
| Device Profile | `common/data/src/main/java/org/thingsboard/server/common/data/DeviceProfile.java` |
| Telemetry | `common/data/src/main/java/org/thingsboard/server/common/data/kv/` |
| MQTT Handler | `common/transport/mqtt/src/main/java/org/thingsboard/server/transport/mqtt/MqttTransportHandler.java` |
| Rule Engine | `rule-engine/rule-engine-components/src/main/java/org/thingsboard/rule/engine/` |
| REST Controllers | `application/src/main/java/org/thingsboard/server/controller/` |
| WebSocket | `application/src/main/java/org/thingsboard/server/service/ws/` |

---

## Recovery Instructions

If starting a new session, use this prompt:

```
Continue documenting the ThingsBoard platform.

Current status:
- Working directory: ~/work/viaanix/claude-thingsboard-docs
- ThingsBoard source: ~/work/viaanix/thingsboard
- Check ROADMAP.md for progress

Next task: [Check the first ⏳ Pending item in the current phase]

Guidelines:
- Technology-agnostic language (behavior/contracts, not Java specifics)
- Include mermaid diagrams in every document
- Target audience: junior developers
- Update ROADMAP.md after completing each document
```

---

## Changelog

### 2026-01-10 (Session 4)
- Created Alarm Entity documentation (`02-core-concepts/entities/alarm.md`)
  - Documented alarm data structure with all fields (severity, status, timestamps, propagation)
  - Explained dual-flag lifecycle (acknowledged + cleared = 4 status combinations)
  - Included mermaid diagrams for severity scale, state transitions, condition types, propagation flow
  - Covered alarm triggers: rule chain conditions (SIMPLE, DURATION, REPEATING), manual API creation
  - Documented deduplication behavior (one active alarm per type/originator)
  - Explained comment system (SYSTEM auto-generated, OTHER user notes)
  - Covered propagation to parent entities with configuration options
  - Documented all operations (acknowledge, clear, assign, unassign)
  - Listed REST API endpoints for retrieval, modification, and utilities

### 2026-01-10 (Session 3)
- Created Asset Entity documentation (`02-core-concepts/entities/asset.md`)
  - Documented asset data structure and JSON format
  - Explained asset profiles and their purpose
  - Included mermaid diagrams for hierarchy, lifecycle, and data aggregation patterns
  - Covered REST API endpoints, bulk import, and name conflict handling
  - Documented entity relations and asset vs device comparison
- Created Tenant Entity documentation (`02-core-concepts/entities/tenant.md`)
  - Documented tenant data structure, profile system, and authority model
  - Included mermaid diagrams for profile configuration, authority hierarchy, isolation
  - Covered multi-tenancy isolation mechanisms (database, API, queue, cache)
  - Documented tenant lifecycle (creation, update, deletion with cascade)
  - Explained quota tracking, rate limits, and usage categories
- Created Customer Entity documentation (`02-core-concepts/entities/customer.md`)
  - Documented customer data structure and entity hierarchy
  - Included mermaid diagrams for resource assignment, public customer, lifecycle
  - Covered device/asset/dashboard assignment patterns
  - Explained public customer concept and unauthenticated dashboard access
  - Documented cascade deletion behavior and access control matrix
- Created Dashboard Entity documentation (`02-core-concepts/entities/dashboard.md`)
  - Documented dashboard data structure (DashboardInfo and full Dashboard)
  - Explained configuration structure (widgets, layouts, aliases, states)
  - Included mermaid diagrams for configuration, customer assignment, home dashboard
  - Covered public dashboard functionality and mobile features
  - Documented REST API endpoints and access control

### 2026-01-10 (Session 2)
- **Comprehensive documentation update based on exploration agent findings**
- Updated authentication.md: API Keys, device credentials, security filter chain, audit logging, rate limiting
- Updated rest-api-overview.md: 57 controllers count, RPC versioning, HAProxy rate limiting
- Updated websocket-overview.md: Session tracking, pending session cache, gRPC Edge communication
- Updated database-schema.md: HikariCP connection pooling, Redis/Caffeine caching layer
- Updated microservices/README.md: Zookeeper discovery details, HAProxy load balancing configuration
- Updated angular-architecture.md: Angular 18.2.13 technology stack, NgRx feature modules
- Updated widget-system.md: Comprehensive WidgetContext services (40+ injected services)
- Updated actor-system/README.md: TbActorSystem implementation, dispatcher configuration
- Updated rule-engine/README.md: 60+ nodes, queue processing strategies (submit/processing)

### 2026-01-10
- Scanned ThingsBoard 4.3.0-RC codebase for documentation updates
- Added Technology Stack section to system-overview.md (Java 17, Spring Boot 3.4.10, Kafka 3.9.1)
- Created entity-types-overview.md documenting all 27 entity types
- Created calculated-fields.md for new v4.x Calculated Fields feature
- Updated actor system README with new actors (CalculatedFieldManagerActor, CalculatedFieldEntityActor, StatsActor)
- Updated microservices README with additional services (Monitoring, Web UI)
- Updated queue-architecture.md with Queue Factory implementations
- Identified new entity types: CALCULATED_FIELD, JOB, AI_MODEL, API_KEY
- **Comprehensive codebase scan completed via 11 parallel exploration agents**

**Agent Exploration Findings:**

**API Layer (57 REST Controllers):**
- Device API, Telemetry API, RPC API (v1 deprecated, v2 current)
- WebSocket endpoints at `/api/ws/**` with JWT authentication
- gRPC services for Edge communication (edge.proto, queue.proto)
- Swagger/OpenAPI documentation via SpringDoc

**Security Implementation:**
- JWT authentication (HS512 algorithm) with refresh tokens
- OAuth2 support (GitHub, Apple, custom mappers)
- API Key / Personal Access Token authentication
- Two-Factor Authentication (TOTP, Email, SMS, Backup codes)
- Device credentials: ACCESS_TOKEN, X509_CERTIFICATE, MQTT_BASIC, LWM2M_CREDENTIALS
- Comprehensive audit logging with Elasticsearch sink support

**Persistence Layer:**
- PostgreSQL (entities), Cassandra (time-series), TimescaleDB (time-series)
- HikariCP connection pooling with configurable leak detection
- Redis/Valkey and Caffeine caching strategies
- SQL partitioning: DAYS, MONTHS, YEARS, INDEFINITE

**Message Queue:**
- Kafka primary implementation with In-Memory for monolith
- Hash-based partitioning (murmur3_128, sha256 options)
- Consumer services: Core, RuleEngine, Edge, CalculatedField
- Topic structure: tb_core, tb_rule_engine.*, tb_transport.*, tb_edge

**Microservices Architecture:**
- Services: tb-node, mqtt/http/coap/lwm2m/snmp transports, js-executor, web-ui, vc-executor, edqs, monitoring
- Zookeeper-based service discovery
- HAProxy load balancing (round-robin, least-conn, source-sticky)
- Docker Compose with replica configurations

**Frontend (Angular 18.2.13):**
- NgRx state management (auth, settings, notifications)
- Widget system with WidgetContext injection (40+ services)
- Dashboard framework with angular-gridster2 layout engine
- WebSocket services for real-time telemetry/notifications
- 64+ TypeScript model files, 40+ HTTP services

### 2026-01-09
- Initial roadmap created
- Phase 1 complete (6 documents)
- Phase 2 started (telemetry complete)
- Attributes documentation complete (8/31 documents, 26%)
- Transport contract documentation complete (9/31 documents, 29%)
- MQTT protocol documentation complete (10/31 documents, 32%)
- Message queue architecture complete - Phase 2 finished (11/31 documents, 35%)
- Rule engine overview complete - Phase 3 started (12/31 documents, 39%)
- Rule chain structure documentation complete (13/31 documents, 42%)
- Message flow (TbMsg) documentation complete (14/31 documents, 45%)
- Node categories documentation complete (15/31 documents, 48%)
- Node development contract complete - Phase 3 finished (16/31 documents, 52%)
- REST API overview complete - Phase 4 started (17/31 documents, 55%)
- Authentication (JWT) documentation complete (18/31 documents, 58%)
- Device API documentation complete (19/31 documents, 61%)
- WebSocket Overview documentation complete (20/31 documents, 65%)
- Subscription Model documentation complete - Phase 4 finished (21/31 documents, 68%)
- Database Schema documentation complete - Phase 5 started (22/31 documents, 71%)
- Time-Series Storage documentation complete (23/31 documents, 74%)
- Multi-Tenancy documentation complete (24/31 documents, 77%)
- Microservices documentation complete (25/31 documents, 81%)
- Queue Partitioning documentation complete - Phase 5 finished (26/31 documents, 84%)
- Angular Architecture documentation complete - Phase 6 started (27/31 documents, 87%)
- Widget System documentation complete (28/31 documents, 90%)
- CoAP Protocol documentation complete (29/32 documents, 91%)
- HTTP Protocol documentation complete (30/32 documents, 94%)
- LwM2M Protocol documentation complete (31/32 documents, 97%)
- SNMP Protocol documentation complete - Phase 6 finished (32/32 documents, 100%)
- All core documentation complete!
