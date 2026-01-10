# System Overview

## Overview

ThingsBoard is a multi-tenant IoT platform that collects data from devices, processes it through configurable rule chains, stores it in databases, and presents it to users via dashboards. The platform handles millions of devices and messages through a scalable, distributed architecture.

## Technology Stack

| Component | Technology | Version |
|-----------|------------|---------|
| Language | Java | 17 |
| Framework | Spring Boot | 3.4.10 |
| Message Queue | Apache Kafka | 3.9.1 |
| Time-Series DB | Apache Cassandra | 4.17.0 |
| Relational DB | PostgreSQL | 15+ |
| Cache | Valkey/Redis | 7+ |
| RPC | gRPC | 1.76.0 |
| Serialization | Protocol Buffers | 3.25.5 |
| Networking | Netty | 4.1.128 |
| Frontend | Angular | 18+ |
| Service Discovery | Apache ZooKeeper | 3.9.3 |

## High-Level Architecture

```mermaid
graph TB
    subgraph "Device Layer"
        D1[IoT Device]
        D2[IoT Device]
        GW[Gateway Device]
        D3[Child Device]
        D4[Child Device]
    end

    subgraph "Transport Layer"
        MQTT[MQTT Transport]
        HTTP[HTTP Transport]
        COAP[CoAP Transport]
        LWM2M[LwM2M Transport]
        SNMP[SNMP Transport]
    end

    subgraph "Message Queue"
        Q[Message Broker]
    end

    subgraph "Processing Layer"
        RE[Rule Engine]
        JS[Script Executor]
    end

    subgraph "Core Services"
        API[REST API]
        WS[WebSocket Server]
        CORE[Core Services]
    end

    subgraph "Storage Layer"
        SQL[(Relational DB)]
        TS[(Time-Series DB)]
        CACHE[(Cache)]
    end

    subgraph "User Layer"
        UI[Web Dashboard]
        EXT[External Systems]
    end

    D1 --> MQTT
    D2 --> HTTP
    GW --> MQTT
    D3 -.->|via gateway| GW
    D4 -.->|via gateway| GW

    MQTT --> Q
    HTTP --> Q
    COAP --> Q
    LWM2M --> Q
    SNMP --> Q

    Q --> RE
    RE <--> JS
    RE --> Q

    Q --> CORE
    CORE --> SQL
    CORE --> TS
    CORE --> CACHE

    API --> CORE
    WS --> CORE

    UI --> API
    UI --> WS
    EXT --> API
```

## Component Responsibilities

### Transport Layer
Handles device connections and protocol translation.

| Component | Protocol | Responsibility |
|-----------|----------|----------------|
| MQTT Transport | MQTT 3.1.1/5.0 | Publish/subscribe messaging, session management |
| HTTP Transport | HTTP/HTTPS | REST-style device API, one-shot requests |
| CoAP Transport | CoAP | Constrained device communication over UDP |
| LwM2M Transport | LwM2M | Device management, object model mapping |
| SNMP Transport | SNMP v2c/v3 | Network device monitoring, polling/traps |

All transports perform:
1. **Authentication** - Validate device credentials
2. **Protocol Translation** - Convert to internal message format (TbMsg)
3. **Session Management** - Track connected devices
4. **Rate Limiting** - Protect against device flooding

### Message Queue
Decouples producers from consumers, enabling scalability.

- **Topics** organize messages by type and destination
- **Partitioning** distributes load across cluster nodes
- **Consumer Groups** enable parallel processing
- **Durability** prevents message loss during failures

### Rule Engine
Processes messages through configurable node chains.

```mermaid
graph LR
    IN[Incoming TbMsg] --> F[Filter Node]
    F -->|match| T[Transform Node]
    F -->|no match| DROP[Drop]
    T --> A1[Save Telemetry]
    T --> A2[Create Alarm]
    T --> A3[Send to External]
```

Key behaviors:
- Each tenant has a default "root" rule chain
- Device profiles can override the rule chain
- Nodes process messages asynchronously
- Failed nodes can route to error handlers

### Core Services
Business logic and data management.

| Service | Responsibility |
|---------|----------------|
| Device Service | Device CRUD, credentials, state tracking |
| Telemetry Service | Time-series data storage and retrieval |
| Alarm Service | Alarm lifecycle (create, ack, clear) |
| Relation Service | Entity relationship management |
| Dashboard Service | Dashboard/widget configuration |
| User Service | Authentication, authorization |
| Notification Service | Email, SMS, push notifications |

### Storage Layer

**Relational Database** (PostgreSQL):
- Entity metadata (devices, assets, users)
- Configuration (rule chains, dashboards)
- Relationships and hierarchies
- Audit logs

**Time-Series Database** (PostgreSQL or Cassandra):
- Telemetry data with timestamps
- Optimized for range queries
- Configurable retention (TTL)

**Cache**:
- Session data
- Frequently accessed entities
- Rate limiting counters

### API Layer
External interfaces for users and integrations.

**REST API**:
- CRUD operations on all entities
- JWT authentication
- Pagination via PageLink
- Role-based access control

**WebSocket API**:
- Real-time telemetry subscriptions
- Alarm notifications
- Dashboard live updates

## Data Flow: Device Telemetry

```mermaid
sequenceDiagram
    participant D as Device
    participant T as Transport
    participant Q as Queue
    participant RE as Rule Engine
    participant C as Core
    participant DB as Database
    participant WS as WebSocket
    participant UI as Dashboard

    D->>T: POST telemetry (MQTT/HTTP)
    T->>T: Authenticate device
    T->>T: Parse payload
    T->>Q: Publish TbMsg

    Q->>RE: Deliver to rule chain
    RE->>RE: Execute filter nodes
    RE->>RE: Execute transform nodes
    RE->>C: Save telemetry action
    C->>DB: Write time-series

    C->>WS: Notify subscribers
    WS->>UI: Push update
    UI->>UI: Refresh widget
```

## Data Flow: Server-to-Device RPC

```mermaid
sequenceDiagram
    participant UI as Dashboard
    participant API as REST API
    participant C as Core
    participant Q as Queue
    participant RE as Rule Engine
    participant T as Transport
    participant D as Device

    UI->>API: POST /rpc/oneway/{deviceId}
    API->>C: Create RPC request
    C->>Q: Publish RPC message
    Q->>RE: Process rule chain
    RE->>T: Route to transport
    T->>D: Deliver command (MQTT/CoAP)
    D->>T: Response (if two-way)
    T->>Q: Publish response
    Q->>C: Deliver response
    C->>API: Return result
    API->>UI: Response
```

## Multi-Tenancy Model

```mermaid
graph TB
    subgraph "Platform"
        SYS[System Admin]
    end

    subgraph "Tenant A"
        TA[Tenant Admin A]
        CA1[Customer A1]
        CA2[Customer A2]
        DA1[Devices]
        DA2[Devices]
    end

    subgraph "Tenant B"
        TB[Tenant Admin B]
        CB1[Customer B1]
        DB1[Devices]
    end

    SYS --> TA
    SYS --> TB
    TA --> CA1
    TA --> CA2
    CA1 --> DA1
    CA2 --> DA2
    TB --> CB1
    CB1 --> DB1
```

**Isolation guarantees:**
- Tenants cannot access each other's data
- Each tenant has separate:
  - Devices and assets
  - Rule chains
  - Dashboards
  - Users and customers
- Database queries always filter by tenant ID
- Actors process messages within tenant context

## Deployment Modes

### Monolithic
Single application instance with embedded services.

```mermaid
graph LR
    subgraph "Single Node"
        APP[Application]
        APP --> DB[(Database)]
        APP --> CACHE[(Cache)]
    end
    DEV[Devices] --> APP
    USER[Users] --> APP
```

**Use case**: Development, small deployments (<10K devices)

### Microservices
Distributed services with message queue coordination.

```mermaid
graph TB
    subgraph "Load Balancer"
        LB[HAProxy/Nginx]
    end

    subgraph "Transport Services"
        T1[MQTT Service 1]
        T2[MQTT Service 2]
        T3[HTTP Service]
    end

    subgraph "Core Services"
        C1[Core Node 1]
        C2[Core Node 2]
    end

    subgraph "Rule Engine"
        RE1[Rule Engine 1]
        RE2[Rule Engine 2]
    end

    subgraph "Support Services"
        JS[JS Executor]
        UI[Web UI]
    end

    subgraph "Infrastructure"
        Q[Message Queue Cluster]
        DB[(Database Cluster)]
        CACHE[(Cache Cluster)]
    end

    LB --> T1
    LB --> T2
    LB --> T3
    LB --> C1
    LB --> C2

    T1 --> Q
    T2 --> Q
    T3 --> Q

    Q --> C1
    Q --> C2
    Q --> RE1
    Q --> RE2

    RE1 <--> JS
    RE2 <--> JS

    C1 --> DB
    C2 --> DB
    C1 --> CACHE
    C2 --> CACHE
```

**Use case**: Production, high availability, >100K devices

## Key Architectural Decisions

### Actor Model for Concurrency
Each device and rule chain has a dedicated actor that processes messages sequentially. This eliminates race conditions and enables millions of concurrent devices without complex locking.

### Message Queue for Decoupling
Asynchronous communication via message queue allows:
- Independent scaling of transports, core, and rule engine
- Fault isolation (failed component doesn't block others)
- Replay capability for recovery

### Configurable Rule Chains
Processing logic is defined as data (rule chains) rather than code. Users can modify behavior without deployments.

### Protocol-Agnostic Core
The core services work with a unified message format (TbMsg). Transport adapters handle protocol-specific details, making it easy to add new protocols.

## See Also

- [Actor System](../03-actor-system/README.md) - Concurrency model details
- [Rule Engine](../04-rule-engine/) - Rule chain architecture
- [Transport Layer](../05-transport-layer/) - Protocol implementations
- [Multi-Tenancy](./multi-tenancy.md) - Isolation details
