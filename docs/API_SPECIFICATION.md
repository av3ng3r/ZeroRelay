# Zerorelay API Specification

## 1. Server WebSocket API

### Connection Endpoint
`ws://<host>:<port>/relay`

### Message Format
All messages follow JSON format with the following general fields:
- `type`: String indicating message type (`connect`, `auth`, `message`, etc.)
- `client_id`: String unique identifier for the client
- `target_id`: String identifier for the message recipient (optional for broadcasts)
- `payload`: Message content (string or structured JSON)
- `timestamp`: ISO 8601 timestamp of message creation

### Connection Lifecycle Messages

#### Connect
- Client initiates WebSocket connection.

#### Authenticate
- Request:
```
{
"type": "auth",
"token": "<auth_token>"
}
```
- Response:
```
{
"type": "auth_response",
"status": "success",
"client_id": "<client_id>"
}
```
or on failure:
```
{
"type": "auth_response",
"status": "failure",
"reason": "<error_message>"
}
```

#### Disconnect
- Client or server may close the connection gracefully or on error.

---

## 2. Messaging API

### Send Message
- Request:
```
{
"type": "message",
"from": "<client_id>",
"to": "<target_id>",
"message_id": "<uuid>",
"payload": "<content>",
"timestamp": "<ISO8601>"
}
```
- Response:
```
{
"type": "message_ack",
"message_id": "<uuid>",
"status": "delivered" | "error",
"reason": "<error_message_optional>"
}
```

### Receive Message
- Server pushes messages in the same format as send request.

---

## 3. Routing API (Internal, Extension)

- Register handlers per protocol/message type.
- Asynchronous dispatch with callbacks for delivery status.

---

## 4. Metrics API

- HTTP Endpoint: `/metrics`
- Exposes Prometheus metrics such as:
  - `zerorelay_active_connections`
  - `zerorelay_messages_sent_total`
  - `zerorelay_auth_failures_total`

---

## 5. Client SDK APIs

### Connect
- Opens WebSocket connection and triggers authentication.

### SendMessage
- Sends a message object to the relay.

### OnMessage
- Event or callback for incoming messages.

### Reconnect
- Automatically handles connection loss and retries with backoff.

---

## 6. Additional Recommendations

- **Error Handling:** Uniform error message format with `type: "error"` and `code`, `message` fields.
- **Heartbeat:** Optional ping/pong message types to maintain connection health.
- **Retry/Deduplication:** Use `message_id` for detecting duplicates and support at-least-once delivery semantics.
- **Extensibility:** Support optional `metadata` or `headers` objects in messages for future protocol features.

---

This API specification provides a clear, modular, and extensible foundation for implementing Zerorelay’s communication protocols aligned with the detailed design.
