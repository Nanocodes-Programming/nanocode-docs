```markdown

# Minimal Call Signaling Guide (WebSocket)

This document outlines the request/response flow for the call-signaling WebSocket used between visitors (guests) and agents, with proper business/department scoping.

---

## WebSocket URLs

- Guest (unauthenticated)
```text
ws://127.0.0.1:8000/ws/signaling/?guest_id=<GUEST_ID>[&business_id=<BUSINESS_ID>]
````

* Agent (authenticated)

```text
ws://127.0.0.1:8000/ws/signaling/?token=<JWT>[&department_id=<DEPT_ID>][&business_id=<BUSINESS_ID>]
```

**Notes:**

* Guests must provide `guest_id`; `business_id` is recommended to scope correctly.
* Agents must connect with a valid JWT. The agent membership is resolved by:

  * `department_id` if provided (must match),
  * else `business_id` (must match exactly one membership),
  * else exactly one membership overall (otherwise rejected).

---

## 1. Connection Established

When the socket is accepted, the server identifies the caller.

* Server → Guest:

```json
{
  "type": "connection_established",
  "guest_id": "2b1b2a9e-4a0a-4e1a-95d6-a6e4b9d9d1b2",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1"
}
```

* Server → Agent:

```json
{
  "type": "connection_established",
  "user_id": 720,
  "agent_id": "a1a2f3b4-5678-49aa-9cde-001122334455",
  "department_id": "7d9a1f32-8c1d-4c29-9e0a-e2a4f7b5c3d1",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1"
}
```

---

## 2. Initiate Call

Two directions are supported. `business_id` is required to scope the call.

* Agent → Guest (Agent → Server):

```json
{
  "type": "call.invite",
  "to_guest_id": "2b1b2a9e-4a0a-4e1a-95d6-a6e4b9d9d1b2",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "caller_display": "Ada Lovelace"
}
```

* Guest → Agent (Guest → Server):

```json
{
  "type": "call.invite",
  "to_agent_id": "44",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "caller_display": "Visitor #42"
}
```

---

## 3. Server Acknowledges Invite

Immediate ACK back to the initiator.

* Server → Agent:

```json
{
  "type": "invite.sent",
  "to_guest_id": "2b1b2a9e-4a0a-4e1a-95d6-a6e4b9d9d1b2",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123"
}
```

* Server → Guest:

```json
{
  "type": "invite.sent",
  "to_agent_id": "a1a2f3b4-5678-49aa-9cde-001122334455",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123"
}
```

---

## 4. Server Notifies Target (Ringing)

* Server → Guest (when invited by an Agent):

```json
{
  "type": "call.ring",
  "from_agent_id": "a1a2f3b4-5678-49aa-9cde-001122334455",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "caller_display": "Ada Lovelace"
}
```

* Server → Agent (when invited by a Guest):

```json
{
  "type": "call.ring",
  "from_guest_id": "2b1b2a9e-4a0a-4e1a-95d6-a6e4b9d9d1b2",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "caller_display": "Visitor #42"
}
```

---

## 5. Respond To Call

Either side can accept or decline. `business_id` and `room_id` must match the invite.

* Agent → Guest (Agent → Server):

```json
{
  "type": "call.response",
  "to_guest_id": "2b1b2a9e-4a0a-4e1a-95d6-a6e4b9d9d1b2",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "accept": true
}
```

* Guest → Agent (Guest → Server):

```json
{
  "type": "call.response",
  "to_agent_id": "a1a2f3b4-5678-49aa-9cde-001122334455",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "accept": false
}
```

---

## 6. Server Acknowledges Response

ACK back to the responder.

* Server → Agent:

```json
{
  "type": "response.sent",
  "to_guest_id": "2b1b2a9e-4a0a-4e1a-95d6-a6e4b9d9d1b2",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "accept": true
}
```

* Server → Guest:

```json
{
  "type": "response.sent",
  "to_agent_id": "a1a2f3b4-5678-49aa-9cde-001122334455",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123",
  "accept": false
}
```

---

## 7. Server Notifies Other Party Of Response

* If accepted:

```json
{
  "type": "call.accepted",
  "from_agent_id": "a1a2f3b4-5678-49aa-9cde-001122334455",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123"
}
```

* If declined:

```json
{
  "type": "call.declined",
  "from_guest_id": "2b1b2a9e-4a0a-4e1a-95d6-a6e4b9d9d1b2",
  "business_id": "8c3d5e71-5d14-4f7b-a6f9-2c90b3c5b8e1",
  "room_id": "room_abc123"
}
```

**Notes:**

* The `from_*` field is `from_agent_id` when the responder is an agent, and `from_guest_id` when the responder is a guest.

---

## Notes

* **Ping/Pong:**

  * Client → Server:

    ```json
    { "type": "ping" }
    ```
  * Server → Client:

    ```json
    { "type": "pong" }
    ```

* All IDs are opaque identifiers.

* `business_id` is required in invite/response messages to avoid cross-business leakage.

* Agents can belong to multiple departments/businesses. On connect, agents must be resolved unambiguously by `department_id` or `business_id` (or have only one membership).

* `room_id` must remain the same across invite and response.

```
