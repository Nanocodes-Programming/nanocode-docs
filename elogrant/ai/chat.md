# AIChatBot API Documentation

## **WebSocket Connection**
The WebSocket connection URL:

`wss://api.elogrants.com/ws/`

## **Authentication**
### **JWT Authentication for WebSockets**
For WebSocket connections, you must pass a valid token in the header as follows:

```
Authorization: Bearer <token>
```

### **Authentication for HTTP Endpoints**
Ensure you pass a valid token in the header as follows:

```
Authorization: Bearer <token>
```

## **Chat WebSocket Endpoint**
### **Endpoint**

```
/chat/
```

This is where you establish a WebSocket connection and initiate a chat session with the AI. Messages are sent and received through this WebSocket.

### **Chat Session Management**
For efficiency, chat history is **not** returned over WebSockets. When initiating a chat session, you are expected to either:
1. Provide an existing `session_id` to continue a conversation.
2. If no `session_id` is provided, a new one will be created and returned upon the first connection.

### **Chat Flow**
1. First, fetch the chat history via HTTP (see the elogrants HTTP API documentation for details).
2. If continuing a previous chat, retrieve the session history via HTTP and get the relevant `session_id`.
3. When connecting via WebSocket, send the `session_id` to continue the session.
4. If no `session_id` is sent, a new session is created and returned upon connection.
5. Messages are sent and received in the following format:

#### **Message Format**
**Request:**
```json
{
  "message": "Hello AI!",
  "session_id": "<session_id>"
}
```

**Response:**
```json
{
  "message": "Hello! How can I assist you today?",
  "session_id": "<session_id>"
}
```

### **Response When No `session_id` is Provided**
If connection is made without providing a `session_id`, a new session will be created, and the response will include the generated `session_id`:

**Response:**
```json
{
  "session_id": "generated_session_id"
}
```

This ensures the user is assigned a valid session before interacting with the AI.

### **In case you wondering why I did not return Chat History Over WebSockets?**
WebSockets are optimized for real-time, event-driven communication, making them ideal for live interactions but inefficient for retrieving historical data. Fetching past messages over WebSockets would:
- Introduce unnecessary overhead, increasing latency and memory usage.
- Require additional logic for pagination, filtering, and state management.
- Impact performance and scalability, especially in high-traffic scenarios.

Instead, chat history retrieval is handled via HTTP, which is better suited for structured queries and database transactions. WebSockets are used exclusively for new messages to ensure optimal performance and a smooth user experience.

### **Session ID Endpoint**
If you need to continue an existing chat session, retrieve the session history via HTTP and use the following WebSocket parameter:

```
/chat/?session_id=<session_id>
```

