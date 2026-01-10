# Documentation Roadmap

This file tracks documentation progress for the ThingsBoard platform rewrite preparation.

**Last Updated**: 2026-01-09

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
| Asset Entity | ⏳ Pending | `02-core-concepts/entities/asset.md` |
| Tenant Entity | ⏳ Pending | `02-core-concepts/entities/tenant.md` |
| Customer Entity | ⏳ Pending | `02-core-concepts/entities/customer.md` |
| Dashboard Entity | ⏳ Pending | `02-core-concepts/entities/dashboard.md` |
| Alarm Entity | ⏳ Pending | `02-core-concepts/entities/alarm.md` |
| Entity Relations | ⏳ Pending | `02-core-concepts/entities/relations.md` |

### Core Concepts - Data Model
| Document | Status | Path |
|----------|--------|------|
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
- [ ] Alarm Lifecycle Flow
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
