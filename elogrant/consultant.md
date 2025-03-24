markdown

# Consultant Chat API Documentation

## Overview
This API enables real-time chat between clients and consultants. It uses a hybrid approach:
- **HTTP Endpoints**: Manage chat session lifecycle (start, end).
- **WebSocket Endpoint**: Handle real-time messaging during active sessions.

Sessions are persistent: a single session per `(consultant, client, service)` trio can be reactivated from `completed` to `active` to continue the conversation, preserving chat history.

## Base URL
- **HTTP**: `https://api.elogrants.com/`
- **WebSocket**: `wss://api.elogrants.com/ws/`

## Authentication
### HTTP Endpoints
Include a valid JWT token in the request header:

Authorization: Bearer <token>

### WebSocket Connections
Pass the JWT token via the `Sec-WebSocket-Protocol` header:

Sec-WebSocket-Protocol: Bearer, <token>

## HTTP Endpoints
NB: For a better understanding of the http endpoints, refer to the normal docs

### 1. Start or Reactivate a Chat Session
Initiates a new chat session or reactivates an existing one with a consultant for a specific service.

#### Endpoint

POST /chats/initiate-session/

#### Request
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "consultant_id": "<consultant_uuid>",
    "service_id": "<service_uuid>"
  }
  ```

- **Response**:

Success (200):
  ```json

    {
      "message": "Session started or reactivated",
      "data": {
        "session_id": "<session_uuid>"
      }
    }
```

If no prior session exists, a new one is created and set to active.

If a session exists:
pending or active: Returns as-is.

completed: Reactivates to active.

- **Error (400/401/403)**:

```json

{
  "message": "<error_description>"
}
```

- **400: Invalid consultant_id or service_id.**
- **401: Missing or invalid token.**
- **403: Unauthorized user.**


**Notes**:

- Use the returned session_id to connect to the WebSocket for real-time chat.
- Only one session exists per (consultant, client, service) due to uniqueness constraints, ensuring continuity.

## 2. End a Chat Session
Ends an active or paused chat session, marking it as completed.

Endpoint

POST /chats/end-session/

#### Request
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "session_id": "<session_uuid>"
  }
  ```


- **Response**:

Success (200):
  ```json

    {
      "message": "Session ended successfully",
      "data": {
        "session_id": "<session_uuid>"
      }
    }
```


Session status changes to completed, and all connected WebSocket clients are disconnected.

```json

{
  "message": "<error_description>"
}
```

- **400: Session already completed.**
- **403: Only the consultant can end the session.**
- **404: Session not found.**


**Notes**
- Triggers a WebSocket broadcast (session_ended) to disconnect all clients in the session.


# WebSocket Endpoint
### Endpoint

/consultant-chat/

Connect to this endpoint for real-time messaging within an active chat session.

### Connection URL

wss://api.elogrants.com/ws/consultant-chat/?session_id=<session_uuid>

- **Query Parameter: session_id from the initiate-session response.**
- **Header: Sec-WebSocket-Protocol: Bearer, <token>**

## Session Management
- Sessions must be active to connect.
- Chat history is not sent over WebSocket—fetch it via HTTP if needed.

## Chat Flow
1. Initiate Session: Use POST /consultant-chats/initiate-session/ to get a session_id.

2. Connect: Open a WebSocket connection with the session_id.

3. Messaging: Send and receive messages in real-time.

4. End Session: Consultant uses POST /consultant-chats/end-session/ to terminate, disconnecting all clients.

## Message Formats

### 1. Connection Established
Sent to the client upon successful WebSocket connection.
```json

{
  "type": "connection_established",
  "session_id": "<session_uuid>"
}
```

### 2. Sending a Text Message
### Request:

``` json
{
  "type": "text",
  "content": "Hello, how can I help you today?"
}
```

### Response (Broadcast to Others):
``` json
{
  "type": "text",
  "content": "Hello, how can I help you today?",
  "sender_id": "<user_uuid>",
  "timestamp": "2025-03-23T12:34:56.789Z"
}
```

### 3. Sending a File Message

### Request:

``` json
{
  "type": "file",
  "file": "https://example.com/uploads/document.pdf",
  "file_name": "document.pdf",
  "is_audio": false
}
```

### Response (Broadcast to Others):

```json
{
  "type": "file",
  "file": "https://example.com/uploads/document.pdf",
  "file_name": "document.pdf",
  "is_audio": false,
  "sender_id": "<user_uuid>",
  "timestamp": "2025-03-23T12:35:00.123Z"
}
```

Note: Ensure the file is uploaded separately (e.g., via an HTTP endpoint) and the URL is sent here.

### 4. Session Ended
### Broadcast when the consultant ends the session.

```json

{
  "type": "session_ended",
  "message": "The consultant has ended this session.",
  "timestamp": "2025-03-23T12:40:00.000Z"
}
```

- Closes the WebSocket connection (code 4006).

### 5. Error
### Sent for invalid actions (e.g., sending after session ends).
``` json
{
  "type": "error",
  "message": "This session has ended. No further communication is allowed."
}
```


> **Notes:**
> - **Session Continuity**: A single session per (consultant, client, service) is reactivated if completed. Use the returned `session_id` to maintain context.
> - **Chat History**: Not provided via WebSocket—implement an HTTP endpoint (Check the normal doc to see the endpoints) if needed.
> - **Error Handling**: Handle WebSocket closure (e.g., code `4006` for `session_ended`) and HTTP errors gracefully.
> - **File Uploads**: Upload files via a separate HTTP endpoint as in the doc and pass the URL in the file message.

