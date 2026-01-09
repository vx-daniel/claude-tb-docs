# Glossary

Terminology used throughout this documentation.

## IoT Fundamentals

### Telemetry
Time-series data sent from devices to the platform. Examples: temperature readings, GPS coordinates, sensor values. Telemetry is typically high-volume, append-only data that gets stored with timestamps.

### Attributes
Key-value pairs that describe device state or configuration. Three types exist:
- **Client Attributes**: Set by the device (e.g., firmware version)
- **Server Attributes**: Set by the platform (e.g., configuration settings)
- **Shared Attributes**: Bidirectional sync between device and platform

### RPC (Remote Procedure Call)
Commands sent between the platform and devices:
- **Server-side RPC**: Platform sends command to device, waits for response
- **Client-side RPC**: Device initiates request to platform

### Provisioning
The process of registering a new device with the platform, including credential assignment and initial configuration.

### OTA (Over-the-Air)
Remote firmware or software updates pushed to devices without physical access.

### Gateway
A device that acts as a bridge between the platform and other devices that cannot connect directly. The gateway manages multiple "child" devices.

### Edge
Computing resources deployed close to devices (on-premises or at network edge) that process data locally before sending to the cloud.

## Communication Protocols

### MQTT
Message Queuing Telemetry Transport. Lightweight publish/subscribe protocol designed for IoT. Devices publish to topics, and the platform subscribes to receive data.

### CoAP
Constrained Application Protocol. REST-like protocol for resource-constrained devices. Uses UDP instead of TCP for lower overhead.

### LwM2M
Lightweight Machine-to-Machine. Device management protocol built on CoAP. Defines standard objects for device info, connectivity, firmware updates.

### SNMP
Simple Network Management Protocol. Used for monitoring network devices. Supports polling (GET) and traps (unsolicited alerts).

## Platform Concepts

### Tenant
An isolated organization within the platform. All data, devices, and users belong to a tenant. Tenants cannot access each other's data.

### Customer
A sub-division within a tenant. Tenants can create customers and assign devices/dashboards to them. Customers have limited permissions compared to tenant administrators.

### Device Profile
A template that defines how devices of a certain type behave:
- Transport configuration (protocol, payload format)
- Alarm rules
- Provisioning settings
- Default rule chain

### Asset
A logical entity representing physical or virtual objects (buildings, production lines, vehicles). Assets can have telemetry, attributes, and relationships to devices.

### Entity
Generic term for any first-class object in the platform: Device, Asset, Tenant, Customer, User, Dashboard, etc. Each entity has a unique ID.

### Entity Relation
A directed connection between two entities. Types include "Contains", "Manages", "Uses". Relations enable hierarchy modeling and data aggregation.

### Dashboard
A container for widgets that visualize data. Dashboards can be assigned to customers and support real-time updates via WebSocket.

### Widget
A visualization component within a dashboard (charts, maps, tables, controls). Widgets subscribe to entity data and update automatically.

## Rule Engine

### Rule Chain
A directed graph of processing nodes that handle incoming messages. Each tenant has a "root" rule chain that processes all device data by default.

### Rule Node
A single processing step in a rule chain. Nodes can filter, transform, enrich, or route messages. Examples: "Filter by device type", "Save telemetry", "Send email".

### TbMsg
The internal message format that flows through rule chains. Contains:
- Type (e.g., POST_TELEMETRY_REQUEST)
- Originator (entity that triggered the message)
- Payload (JSON data)
- Metadata (key-value context)

### Message Type
Classification of what triggered a message. Common types:
- `POST_TELEMETRY_REQUEST` - Device sent telemetry
- `POST_ATTRIBUTES_REQUEST` - Device updated attributes
- `RPC_CALL_FROM_SERVER_TO_DEVICE` - Server-initiated RPC
- `ACTIVITY_EVENT` - Device connected/disconnected

## Runtime Concepts

### Actor
A concurrent processing unit that handles messages sequentially. Each device and rule chain has its own actor, preventing race conditions and enabling scalability.

### Actor Mailbox
The queue of pending messages for an actor. Messages are processed one at a time in order.

### Partition
A subset of data or processing assigned to a specific node in a cluster. Partitioning enables horizontal scaling.

## Data Storage

### Time-Series Database
Storage optimized for timestamped data. Supports efficient range queries (e.g., "last 24 hours of temperature data").

### Key-Value Store
Storage for attributes and entity metadata. Supports point queries (e.g., "get device firmware version").

### TTL (Time-to-Live)
Automatic expiration of old data. Telemetry can be configured to delete after a retention period.

## API Concepts

### JWT (JSON Web Token)
Authentication token containing encoded user identity and permissions. Passed in HTTP headers for API requests.

### WebSocket Subscription
A persistent connection for real-time data updates. Clients subscribe to entities/attributes and receive push notifications when data changes.

### Page Link
Pagination mechanism for list queries. Contains page size, page number, and optional sorting/filtering parameters.

## See Also

- [System Overview](./01-architecture/system-overview.md) - How these concepts fit together
- [Device Entity](./02-core-concepts/entities/device.md) - Deep dive on devices
- [Rule Engine](./04-rule-engine/) - Rule chain documentation
