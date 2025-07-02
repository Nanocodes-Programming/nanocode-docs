# Live Chat API Documentation (Visitor Support System)

## Overview
This API enables **real-time live chat** between **website visitors** and **merchant agents**.

It uses a hybrid structure:
- **HTTP Endpoints**: for initiating sessions, uploading files, and viewing chat history.
- **WebSocket Endpoint**: for real-time messaging between visitors and agents.

---

## Base URLs

- **HTTP**: `https://api.andromedia.com/`
- **WebSocket**: `wss://api.andromedia.com/ws/visitor-chat/`

---

## Authentication

### HTTP Endpoints
- Use **public access** for visitors and **JWT token** for agents.

### WebSocket (Visitor & Agent)
Pass JWT token via the `Sec-WebSocket-Protocol` header:

```
Sec-WebSocket-Protocol: Bearer, <token>
```

---

## HTTP Endpoints

### 1. Start Chat Session

Start or retrieve a chat session between a visitor and a merchant (business).

**POST** `/chat/start-session/`

#### Request
```json
{
  "business": "<business_id>",
  "department": "<department_id (optional)>",
  "external_customer_id": "<optional_customer_id>"
}
```

#### Response
```json
{
  "message": "Chat session started successfully",
  "data": {
    "session_id": "<session_uuid>",
    "active": true
  }
}
```

---

### 2. Upload a File

Used to upload a file before sending it in WebSocket chat.

**POST** `/chat/upload-file/`

#### Headers
- Content-Type: multipart/form-data

#### Body Fields
- `file`: (binary)
- `message`: ID of the related ChatMessage (or null)
- `uploaded_by_end_user`: UUID
- `uploaded_by_agent`: UUID (optional)

#### Response
```json
{
  "message": "File uploaded successfully",
  "data": {
    "file": "https://andromedia.com/media/chat_attachments/example.pdf",
    "file_name": "example.pdf"
  }
}
```

---

### 3. Get Chat History

**GET** `/chat/history/<session_id>/`

Returns a combined list of messages and attachments.

#### Response
```json
{
  "message": "Chat timeline fetched successfully",
  "data": [
    { "type": "message", "data": { ... } },
    { "type": "attachment", "data": { ... } }
  ]
}
```

---

## WebSocket: Real-Time Chat

**Endpoint**: `/ws/visitor-chat/?session_id=<session_uuid>`

- Authenticated via `Sec-WebSocket-Protocol`
- Session must be active

---

### 1. Connection Established

```json
{
  "type": "connection_established",
  "session_id": "<session_uuid>"
}
```

---

### 2. Send a Text Message

#### Client → Server
```json
{
  "type": "text",
  "content": "Hello, I need help!"
}
```

#### Server → Broadcast to group
```json
{
  "type": "text",
  "content": "Hello, I need help!",
  "sender_id": "<user_uuid>",
  "timestamp": "2025-07-02T12:00:00.000Z"
}
```

---

### 3. Send a File Message

#### Client → Server
```json
{
  "type": "file",
  "file": "https://andromedia.com/media/chat_attachments/example.pdf",
  "is_audio": false
}
```

#### Server → Broadcast
```json
{
  "type": "file",
  "file": "https://andromedia.com/media/chat_attachments/example.pdf",
  "file_name": "example.pdf",
  "is_audio": false,
  "sender_id": "<user_uuid>",
  "timestamp": "2025-07-02T12:02:00.000Z"
}
```

---

### 4. Session Ended (Broadcast Only)

```json
{
  "type": "session_ended",
  "message": "The session has ended.",
  "timestamp": "2025-07-02T12:10:00.000Z"
}
```

- Triggers client-side disconnect.
- WebSocket closes with code `4006`.

---

### 5. Error Message

```json
{
  "type": "error",
  "message": "This session has ended. No further communication is allowed."
}
```

---

## WebSocket Disconnection Codes

| Code   | Reason                     |
|--------|----------------------------|
| 4001   | Missing session_id         |
| 4002   | Invalid session_id         |
| 4003   | Unauthorized access        |
| 4006   | Session has ended          |

---

## Notes

- **Only 1 active session** per guest or external customer per business.
- Files must be uploaded first via HTTP, then their URL used in WebSocket.
- Agents and visitors are both authenticated separately using JWT.
- Chat history is not sent via WebSocket—fetch via HTTP.