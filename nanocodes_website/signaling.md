# Minimal Call Signaling Guide (WebSocket)

This document outlines the **request/response flow** for the minimal call-signaling WebSocket used between **students** and **mentors/tutors**.

---

## WebSocket URL

```text
ws://127.0.0.1:8000/ws/signaling/?token=<JWT>
```

- Replace `<JWT>` with the authenticated user token.
- The token is used to authenticate the connection.

---

## 1. Connection Established

When a client connects with a valid JWT:

**Server → Student:**

```json
{
  "type": "connection_established",
  "user_id": 720
}
```

- `user_id` is the authenticated student's CustomUser ID.

---

## 2. Student Initiates Call

**Student → Server:**

```json
{
  "type": "call.invite",
  "to_user_id": 5,          // ID of the Mentor/Tutor
  "target_type": "mentor",  // "mentor" or "tutor"
  "room_id": "room_abc123", // Unique room identifier
  "caller_display": "Samuel Osondu" // Optional display info
}
```

- `to_user_id`: ID of the mentor/tutor to call.
- `room_id`: Unique identifier for this call session.
- `caller_display`: Display name of the student.

---

## 3. Server Acknowledges Invite to Student

**Server → Student:**

```json
{
  "type": "invite.sent",
  "to_user_id": 5,
  "room_id": "room_abc123",
  "target_type": "mentor"
}
```

- Immediate acknowledgment that the invite was sent.

---

## 4. Server Notifies Mentor/Tutor

**Server → Mentor/Tutor:**

```json
{
  "type": "call.ring",
  "from_user_id": 720,
  "room_id": "room_abc123",
  "caller_display": "Samuel Osondu: Student!",
  "target_type": "tutor"
}
```

- `from_user_id`: ID of the student initiating the call.
- `caller_display`: Name or info about the student.
- `target_type`: Indicates whether the recipient is a mentor or tutor.

---

## 5. Mentor/Tutor Responds

**Mentor/Tutor → Server:**

```json
{
  "type": "call.response",
  "to_user_id": 720,
  "room_id": "room_abc123",
  "accept": true
}
```

- `accept`: `true` if they accept, `false` if they decline.

---

## 6. Server Acknowledges Response to Mentor/Tutor

**Server → Mentor/Tutor:**

```json
{
  "type": "response.sent",
  "to_user_id": 720,
  "room_id": "room_abc123",
  "accept": true
}
```

- Confirms that the response was successfully received by the server.

---

## 7. Server Notifies Student of Response

**If Mentor/Tutor Accepted:**

```json
{
  "type": "call.accepted",
  "from_user_id": 5,
  "room_id": "room_abc123"
}
```

**If Mentor/Tutor Declined:**

```json
{
  "type": "call.declined",
  "from_user_id": 5,
  "room_id": "room_abc123"
}
```

- `from_user_id`: ID of the mentor/tutor who responded.
- Student can then proceed to join the call if accepted.

---

## Notes

- **Ping/Pong** events can be sent for connectivity checks:

**Client → Server:**

```json
{ "type": "ping" }
```

**Server → Client:**

```json
{ "type": "pong" }
```

- All IDs sent to the client are **opaque identifiers**.
- `target_type` ensures no conflicts between Mentor and Tutor tables.
- `room_id` must be consistent across invite and response messages.

---

End of Guide

