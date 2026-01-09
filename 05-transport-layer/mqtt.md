# MQTT Protocol

## Overview

MQTT (Message Queuing Telemetry Transport) is the primary device communication protocol in the platform. It provides a lightweight, publish/subscribe messaging model ideal for IoT devices with limited bandwidth and processing power. The platform supports MQTT 3.1.1 and MQTT 5.0, with features including QoS levels 0 and 1, persistent sessions, and bidirectional communication.

## Key Behaviors

1. **Access Token Authentication**: Devices authenticate using access tokens passed as the MQTT username.

2. **X.509 Certificate Authentication**: Devices can authenticate using client certificates for enhanced security.

3. **Two API Versions**: v1 topics use full paths (`v1/devices/me/telemetry`), v2 topics use short paths (`v2/t`) to reduce bandwidth.

4. **Multiple Payload Formats**: Supports JSON (default), Protocol Buffers, and device profile-specific formats.

5. **Bidirectional Communication**: Devices can publish data and subscribe to receive commands, attribute updates, and RPC requests.

6. **Gateway Support**: Gateway devices can manage multiple child devices through dedicated gateway topics.

7. **Sparkplug B Support**: Industrial IoT integration via the Sparkplug B specification.

## Connection Flow

```mermaid
sequenceDiagram
    participant D as Device
    participant M as MQTT Handler
    participant TS as TransportService
    participant CS as Credential Store
    participant DP as Device Profile

    D->>M: CONNECT (username=accessToken)
    M->>TS: ValidateBasicMqttCredRequestMsg
    TS->>CS: Lookup credentials

    alt Valid Credentials
        CS-->>TS: Device info
        TS->>DP: Get device profile
        DP-->>TS: Profile configuration
        TS-->>M: ValidateDeviceCredentialsResponse
        M->>M: Initialize session
        M->>TS: registerAsyncSession
        M-->>D: CONNACK (Success)
    else Invalid Credentials
        CS-->>TS: Not found
        TS-->>M: Validation failed
        M-->>D: CONNACK (Not Authorized)
        M->>M: Close connection
    end
```

## Authentication Methods

### Access Token Authentication

The simplest authentication method. Device passes access token as MQTT username.

| MQTT Field | Value |
|------------|-------|
| Username | Device access token |
| Password | (optional) |
| Client ID | Any unique identifier |

**Example:**
```
Username: A1B2C3D4E5F6G7H8
Password:
ClientId: myDevice001
```

### MQTT Basic Credentials

Uses both username and password for authentication.

| MQTT Field | Value |
|------------|-------|
| Username | Configured username |
| Password | Configured password |
| Client ID | Configured client ID |

### X.509 Certificate Authentication

Devices authenticate using TLS client certificates. The platform validates the certificate fingerprint against registered credentials.

**Requirements:**
- TLS connection required
- Client certificate must be configured in device credentials
- Certificate validity checked (can be disabled via configuration)

## Topic Structure

### v1 Device Topics

Standard topics for individual device communication.

| Operation | Topic | Direction | Payload |
|-----------|-------|-----------|---------|
| Post telemetry | `v1/devices/me/telemetry` | Device → Server | JSON telemetry |
| Post attributes | `v1/devices/me/attributes` | Device → Server | JSON attributes |
| Request attributes | `v1/devices/me/attributes/request/{requestId}` | Device → Server | `{"clientKeys":"k1,k2","sharedKeys":"k3"}` |
| Attribute response | `v1/devices/me/attributes/response/{requestId}` | Server → Device | JSON attributes |
| Subscribe to attributes | `v1/devices/me/attributes` | Server → Device | JSON shared attributes |
| Server RPC request | `v1/devices/me/rpc/request/{requestId}` | Server → Device | `{"method":"name","params":{}}` |
| Server RPC response | `v1/devices/me/rpc/response/{requestId}` | Device → Server | JSON response |
| Client RPC request | `v1/devices/me/rpc/request/{requestId}` | Device → Server | `{"method":"name","params":{}}` |
| Device claim | `v1/devices/me/claim` | Device → Server | `{"secretKey":"...", "durationMs":...}` |

### v2 Short Topics

Bandwidth-efficient topics for constrained devices.

| Operation | Topic | Format Variants |
|-----------|-------|-----------------|
| Post telemetry | `v2/t` | `v2/t/j` (JSON), `v2/t/p` (Protobuf) |
| Post attributes | `v2/a` | `v2/a/j` (JSON), `v2/a/p` (Protobuf) |
| Request attributes | `v2/a/req/{requestId}` | `v2/a/req/j/{id}`, `v2/a/req/p/{id}` |
| Attribute response | `v2/a/res/{requestId}` | `v2/a/res/j/{id}`, `v2/a/res/p/{id}` |
| RPC request (to device) | `v2/r/req/{requestId}` | `v2/r/req/j/{id}`, `v2/r/req/p/{id}` |
| RPC response (from device) | `v2/r/res/{requestId}` | `v2/r/res/j/{id}`, `v2/r/res/p/{id}` |

### Gateway Topics

Topics for gateway devices managing child devices.

| Operation | Topic | Payload |
|-----------|-------|---------|
| Child connect | `v1/gateway/connect` | `{"device":"name"}` |
| Child disconnect | `v1/gateway/disconnect` | `{"device":"name"}` |
| Telemetry (multi-device) | `v1/gateway/telemetry` | `{"Device A":[{...}], "Device B":[{...}]}` |
| Attributes (multi-device) | `v1/gateway/attributes` | `{"Device A":{...}, "Device B":{...}}` |
| Attribute request | `v1/gateway/attributes/request` | `{"id":1, "device":"name", "client":true, "keys":["k1"]}` |
| Attribute response | `v1/gateway/attributes/response` | Response payload |
| RPC response | `v1/gateway/rpc` | `{"device":"name", "id":1, "data":{}}` |
| Device claim | `v1/gateway/claim` | `{"Device A":{"secretKey":"..."}}` |

### Provisioning Topics

For automatic device registration.

| Operation | Topic |
|-----------|-------|
| Provision request | `/provision/request` |
| Provision response | `/provision/response` |

### OTA Update Topics

For firmware and software updates.

| Operation | Topic |
|-----------|-------|
| Firmware request | `v2/fw/request/{requestId}/chunk/{chunk}` |
| Firmware response | `v2/fw/response/{requestId}/chunk/{chunk}` |
| Firmware error | `v2/fw/error` |
| Software request | `v2/sw/request/{requestId}/chunk/{chunk}` |
| Software response | `v2/sw/response/{requestId}/chunk/{chunk}` |
| Software error | `v2/sw/error` |

## Topic Flow Diagram

```mermaid
graph TB
    subgraph "Device Operations"
        PUB_TEL[Publish Telemetry] -->|v1/devices/me/telemetry| SERVER
        PUB_ATTR[Publish Attributes] -->|v1/devices/me/attributes| SERVER
        REQ_ATTR[Request Attributes] -->|v1/devices/me/attributes/request/+| SERVER
    end

    subgraph "Server Operations"
        SERVER -->|v1/devices/me/attributes| SUB_ATTR[Attribute Updates]
        SERVER -->|v1/devices/me/rpc/request/+| RPC_REQ[RPC Requests]
    end

    subgraph "Device Responses"
        RPC_REQ -->|Process| DEVICE
        DEVICE -->|v1/devices/me/rpc/response/+| RPC_RESP[RPC Response]
        RPC_RESP --> SERVER
    end
```

## Payload Formats

### Telemetry Payload

**Simple format (server assigns timestamp):**
```json
{
  "temperature": 25.5,
  "humidity": 60,
  "status": "active"
}
```

**With explicit timestamp:**
```json
{
  "ts": 1634567890123,
  "values": {
    "temperature": 25.5,
    "humidity": 60
  }
}
```

**Multiple timestamps:**
```json
[
  {"ts": 1634567890000, "values": {"temperature": 25.5}},
  {"ts": 1634567891000, "values": {"temperature": 25.7}}
]
```

### Attributes Payload

**Client attributes:**
```json
{
  "firmware_version": "1.2.3",
  "ip_address": "192.168.1.100",
  "hardware_model": "ESP32"
}
```

### RPC Request Payload

**Server to device:**
```json
{
  "method": "setConfiguration",
  "params": {
    "interval": 30,
    "enabled": true
  }
}
```

**Device response:**
```json
{
  "result": "success"
}
```

### Gateway Telemetry Payload

```json
{
  "Sensor A": [
    {"ts": 1634567890123, "values": {"temperature": 25.5}}
  ],
  "Sensor B": [
    {"ts": 1634567890456, "values": {"humidity": 60}}
  ]
}
```

## QoS Support

| QoS Level | Name | Behavior | Supported |
|-----------|------|----------|-----------|
| 0 | At most once | Fire and forget, no acknowledgment | Yes |
| 1 | At least once | Guaranteed delivery with PUBACK | Yes |
| 2 | Exactly once | Guaranteed single delivery | No |

**QoS Selection:**
- The platform caps requested QoS at level 1
- Requested QoS 2 is downgraded to QoS 1
- Server-to-device messages use the subscribed QoS

## Subscription Flow

```mermaid
sequenceDiagram
    participant D as Device
    participant M as MQTT Handler
    participant TS as TransportService
    participant DA as Device Actor

    D->>M: SUBSCRIBE (v1/devices/me/rpc/request/+)
    M->>TS: SubscribeToRPCMsg
    TS->>DA: Register subscription
    DA-->>TS: Confirmed
    M-->>D: SUBACK (granted QoS)

    Note over D,DA: Later, server initiates RPC

    DA->>TS: RPC request
    TS->>M: ToDeviceRpcRequestMsg
    M-->>D: PUBLISH (v1/devices/me/rpc/request/123)
    D->>D: Process RPC
    D->>M: PUBLISH (v1/devices/me/rpc/response/123)
    M->>TS: ToDeviceRpcResponseMsg
    TS->>DA: Deliver response
```

## Message Processing

### Publish Message Handling

```mermaid
graph TB
    MSG[PUBLISH Message] --> PARSE[Parse Topic]

    PARSE --> GW{Gateway Topic?}
    GW -->|Yes| GWHANDLER[Gateway Handler]
    GW -->|No| SP{Sparkplug?}

    SP -->|Yes| SPHANDLER[Sparkplug Handler]
    SP -->|No| DEV[Device Handler]

    DEV --> TOPIC{Topic Type}
    TOPIC -->|telemetry| TEL[PostTelemetryMsg]
    TOPIC -->|attributes| ATTR[PostAttributeMsg]
    TOPIC -->|rpc/response| RPC[ToDeviceRpcResponseMsg]
    TOPIC -->|rpc/request| SRPC[ToServerRpcRequestMsg]
    TOPIC -->|claim| CLAIM[ClaimDeviceMsg]
    TOPIC -->|fw/request| OTA[OTA Package Request]

    TEL --> TS[Transport Service]
    ATTR --> TS
    RPC --> TS
    SRPC --> TS
    CLAIM --> TS
    OTA --> CACHE[OTA Package Cache]
```

### Gateway Message Flow

```mermaid
sequenceDiagram
    participant GW as Gateway
    participant M as MQTT Handler
    participant GH as Gateway Handler
    participant TS as TransportService
    participant DS as Device Service

    GW->>M: PUBLISH v1/gateway/connect
    M->>GH: onDeviceConnect
    GH->>TS: GetOrCreateDeviceFromGatewayRequest
    TS->>DS: Find/create device

    alt Device exists
        DS-->>TS: Existing device
    else Device not found
        DS->>DS: Create device
        DS->>DS: Create "Contains" relation
        DS-->>TS: New device
    end

    TS-->>GH: Device session info
    GH-->>M: Success
    M-->>GW: PUBACK

    Note over GW,DS: Gateway posts telemetry for child

    GW->>M: PUBLISH v1/gateway/telemetry
    M->>GH: onDeviceTelemetry
    GH->>GH: Parse device name from payload
    GH->>TS: PostTelemetryMsg (child session)
    TS-->>GH: Success
    M-->>GW: PUBACK
```

## Sparkplug B Support

The platform supports the Sparkplug B specification for industrial IoT integration.

### Sparkplug Topic Structure

```
spBv1.0/{group_id}/{message_type}/{edge_node_id}[/{device_id}]
```

| Message Type | Description |
|--------------|-------------|
| NBIRTH | Node birth certificate |
| NDEATH | Node death certificate |
| NDATA | Node data |
| NCMD | Node command |
| DBIRTH | Device birth certificate |
| DDEATH | Device death certificate |
| DDATA | Device data |
| DCMD | Device command |

### Sparkplug Flow

```mermaid
sequenceDiagram
    participant EN as Edge Node
    participant M as MQTT Handler
    participant SPH as Sparkplug Handler
    participant TS as TransportService

    EN->>M: CONNECT
    M-->>EN: CONNACK

    EN->>M: SUBSCRIBE spBv1.0/+/NCMD/+
    M-->>EN: SUBACK

    EN->>M: PUBLISH spBv1.0/G1/NBIRTH/E1
    M->>SPH: onAttributesTelemetryProto (NBIRTH)
    SPH->>TS: Process node birth

    EN->>M: PUBLISH spBv1.0/G1/DBIRTH/E1/D1
    M->>SPH: onAttributesTelemetryProto (DBIRTH)
    SPH->>TS: Process device birth

    EN->>M: PUBLISH spBv1.0/G1/DDATA/E1/D1
    M->>SPH: onAttributesTelemetryProto (DDATA)
    SPH->>TS: Process device data
```

## Provisioning Flow

```mermaid
sequenceDiagram
    participant D as New Device
    participant M as MQTT Handler
    participant TS as TransportService
    participant PS as Provisioning Service

    D->>M: CONNECT (username="provision")
    M->>M: Set provision-only mode
    M-->>D: CONNACK

    D->>M: SUBSCRIBE /provision/response
    M-->>D: SUBACK

    D->>M: PUBLISH /provision/request
    Note right of D: {"deviceName":"...", "provisionDeviceKey":"...", "provisionDeviceSecret":"..."}
    M->>TS: ProvisionDeviceRequestMsg
    TS->>PS: Validate and provision

    alt Successful
        PS-->>TS: New credentials
        TS-->>M: ProvisionDeviceResponseMsg
        M-->>D: PUBLISH /provision/response
        Note right of D: {"credentialsType":"ACCESS_TOKEN", "accessToken":"..."}
        M->>M: Schedule disconnect (60s)
    else Failed
        PS-->>TS: Error
        TS-->>M: Error response
        M-->>D: PUBLISH /provision/response
        Note right of D: {"errorMsg":"...", "status":"FAILURE"}
    end
```

## OTA Updates Flow

```mermaid
sequenceDiagram
    participant D as Device
    participant M as MQTT Handler
    participant TS as TransportService
    participant CACHE as OTA Cache

    D->>M: SUBSCRIBE v2/fw/response/+/chunk/+
    M-->>D: SUBACK

    D->>M: PUBLISH v2/fw/request/1/chunk/0
    Note right of D: Payload: chunk size (e.g., "4096")
    M->>TS: GetOtaPackageRequestMsg
    TS-->>M: Package ID

    M->>CACHE: Get chunk 0
    CACHE-->>M: Chunk data
    M-->>D: PUBLISH v2/fw/response/1/chunk/0

    loop For each chunk
        D->>M: PUBLISH v2/fw/request/1/chunk/N
        M->>CACHE: Get chunk N
        CACHE-->>M: Chunk data
        M-->>D: PUBLISH v2/fw/response/1/chunk/N
    end
```

## Session Management

### Session States

```mermaid
stateDiagram-v2
    [*] --> Connecting: CONNECT received
    Connecting --> Authenticating: Parse credentials
    Authenticating --> ProvisionOnly: username="provision"
    Authenticating --> Connected: Valid credentials
    Authenticating --> [*]: Invalid credentials

    ProvisionOnly --> ProvisionOnly: Provisioning topics only
    ProvisionOnly --> [*]: Provisioned or timeout

    Connected --> Connected: PUBLISH/SUBSCRIBE
    Connected --> Connected: PINGREQ/PINGRESP
    Connected --> Disconnecting: DISCONNECT
    Connected --> Disconnecting: Error/Timeout

    Disconnecting --> [*]: Cleanup complete
```

### Keep-Alive

- Devices send PINGREQ to maintain connection
- Server responds with PINGRESP
- Gateway devices trigger ping for all child device sessions
- Activity recorded on each interaction

## Error Handling

### MQTT 5.0 Reason Codes

| Code | Name | When |
|------|------|------|
| 0x00 | SUCCESS | Operation completed |
| 0x80 | UNSPECIFIED_ERROR | Generic failure |
| 0x83 | IMPLEMENTATION_SPECIFIC_ERROR | Internal error |
| 0x87 | NOT_AUTHORIZED | Authentication failed |
| 0x8F | TOPIC_FILTER_INVALID | Invalid subscription topic |
| 0x99 | PAYLOAD_FORMAT_INVALID | Malformed payload |

### Error Responses

| Error Type | MQTT 3.1.1 Behavior | MQTT 5.0 Behavior |
|------------|---------------------|-------------------|
| Invalid payload | Close connection | PUBACK with error code |
| Invalid topic | Close connection | PUBACK with TOPIC_NAME_INVALID |
| Rate limited | Close connection | PUBACK with error code |
| Auth failure | CONNACK refused | CONNACK with reason code |

## Configuration Options

### Device Profile Settings

| Setting | Description | Default |
|---------|-------------|---------|
| transportPayloadType | JSON or PROTOBUF | JSON |
| sendAckOnValidationException | Send PUBACK on errors | false |
| telemetryTopic | Custom telemetry topic pattern | Standard |
| attributesTopic | Custom attributes topic pattern | Standard |

### Transport Settings

| Setting | Description |
|---------|-------------|
| maxPayloadSize | Maximum payload size for OTA chunks |
| skipValidityCheckForClientCert | Skip X.509 validity check |

## Security Considerations

### TLS/SSL

- TLS encryption recommended for production
- Server certificate validation
- Optional client certificate authentication
- Certificate pinning support

### Access Control

- Devices can only access their own topics
- Gateway devices can access child device topics
- Provision-only sessions restricted to provisioning topics

### Rate Limiting

- Per-device message limits
- Per-tenant aggregate limits
- Transport-level global limits
- Exceeding limits results in connection termination

## Implementation Example

### Device Publishing Telemetry

```
# Connect
CONNECT
  Client ID: device001
  Username: A1B2C3D4E5F6

# Publish telemetry
PUBLISH
  Topic: v1/devices/me/telemetry
  QoS: 1
  Payload: {"temperature": 25.5, "humidity": 60}

# Receive acknowledgment
PUBACK
```

### Device Receiving RPC

```
# Subscribe to RPC requests
SUBSCRIBE
  Topic: v1/devices/me/rpc/request/+
  QoS: 1

# Receive SUBACK

# Later, receive RPC request
PUBLISH (from server)
  Topic: v1/devices/me/rpc/request/123
  Payload: {"method": "getValue", "params": {}}

# Send response
PUBLISH
  Topic: v1/devices/me/rpc/response/123
  Payload: {"value": 42}
```

## See Also

- [Transport Contract](./transport-contract.md) - Common transport interface
- [Device Entity](../02-core-concepts/entities/device.md) - Device authentication
- [Telemetry](../02-core-concepts/data-model/telemetry.md) - Data format
- [Attributes](../02-core-concepts/data-model/attributes.md) - Attribute handling
- [CoAP Protocol](./coap.md) - Alternative constrained protocol
- [HTTP Protocol](./http.md) - REST-based alternative
