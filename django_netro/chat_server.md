# API Documentation for the websocket chat server

Api host:

```
wss://api.netroxchange.com/
```

## Endpoint overview

1. **Get messages**

   - `/chat/messages/<uid>/` (GET)

2. **Upload chat with an attachment**

   - `/chat/chat-attachment/` (POST)

3. **Get user threads**
   - `/chat/get-user-threads/` (GET)

# Detailed endpoint documentation

**1. Get Messages**

- **Endpoint**: `/chat/messages/<uid>/`
- **Path Parameters**:
  - `uuid` The id of the user whose conversation messages you want to create.
- **Description:** This endpoints gets the messages in the conversation between the currently logged-in user and the user with the uid specified in the path parameter.

- **Responses:**
  - **200 success:** Data fetched successfully

```json
{
  "status": "success",
  "entity": {
    "messages": [
      {
        "id": 30,
        "sender": {
          "id": "96bf0d3f-720d-4620-8dee-0f59f997cb51",
          "email": "codebee345@outlook.com",
          "profile": null
        },
        "receiver": {
          "id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437",
          "email": "onuhudoudo@gmail.com",
          "profile": null
        },
        "attached_file_size": "0kb",
        "message": "hello",
        "updated": "2024-06-17T11:28:21.902531Z",
        "created": "2024-06-17T11:28:21.902531Z",
        "seen": false,
        "deleted": false,
        "attached_file": null,
        "attached_file_name": null,
        "thread": 1
      },
      {
        "id": 30,
        "sender": {
          "id": "96bf0d3f-720d-4620-8dee-0f59f997cb51",
          "email": "codebee345@outlook.com",
          "profile": null
        },
        "receiver": {
          "id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437",
          "email": "onuhudoudo@gmail.com",
          "profile": null
        },
        "attached_file_size": "0kb",
        "message": "hello",
        "updated": "2024-06-17T11:28:21.902531Z",
        "created": "2024-06-17T11:28:21.902531Z",
        "seen": false,
        "deleted": false,
        "attached_file": null,
        "attached_file_name": null,
        "thread": 1
      }
    ]
  },
  "message": "Messages retreived successfully",
  "success": true
}
```

- **404: not found:**

```json
{
  "status": "failure",
  "entity": null,
  "message": "Invalid receipient",
  "success": false
}
```

**3. Get user threads**

- **Endpoint**: `/chat/get-user-threads/`
- **Permissions:** isAuthenticated
- **Description:** Gets the threads associated with the currently logged-in user. A thread basically respresents a conversation between two users.

- **Resonses:**
  - 200 success
  ```json
  {
    "status": "success",
    "entity": [
      {
        "id": 1,
        "user_one": {
          "id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437",
          "email": "onuhudoudo@gmail.com",
          "profile": null
        },
        "user_two": {
          "id": "96bf0d3f-720d-4620-8dee-0f59f997cb51",
          "email": "codebee345@outlook.com",
          "profile": null
        },
        "craeted": "2024-06-16T11:43:37.563070Z"
      }
    ],
    "message": null,
    "success": true
  }
  ```

## **Connecting and using the websocket**

- **Endpoint**: `/ws/chat/room/`
- **Query Parameters**:
  - `?token=` This is the access token of the currently logged in user.
- **Example url**: `wss://host.com/ws/chat/room/?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`
- **Description:** Establishes a bidirectional websocket connection to the server.

Once connected to the websocket, messages can now be sent to and fro, each message carrying an action field which indicates the operation to be performed

## Sending messages without a file attachment

#### _Step 1. Send a message to the server_

### Message payload: (client to server)

```json
{
  "action": "chat_message",
  "message_body": "hello there",
  "receiver_id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437"
}
```

- **action:** "chat_message" This indicates the message is just a regular message, it does not carry a file
- **receiver_id:** The id of the user supposed to receive this message. When sent, the receiving client will receive the message immediately if they are also logged in and connected to the websocket.
- **message_body:** The text message to be sent

#### _Step 2. Receive message from the server_

### Message response: (server to client):

When a message with the action of `chat_message` is sent, the server stores the message in the database and deliveres it in real time to the user with the specified `receiver_id` if they are logged in and connected to the websocket.

Below is the realtime response that will be received by the specified receiever:

```json
{
  "message_body": "hello",
  "sender_id": "96bf0d3f-720d-4620-8dee-0f59f997cb51",
  "receiver_id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437",
  "timestamp": "2024-06-17T12:48:28.228342+00:00",
  "created_msg_id": 34,
  "action": "re_message"
}
```

- **action:** `re_message` This indicates it is a response message.
- **receiver_id:** The id of the user who is meant to receive the message
- **message_body:** The text content of the message
- **timestamp:** isoFormat time indicating when the message was sent

## Sending messages with a file attachment

Due to the fact that transfering files through a websocket endpoint can be overly resource intensive, it is required to uplaod files to a http endpoint after which the chat message is sent via websocket

#### _Step 1: Upload chat and file to server using http endpoint_

- **Endpoint:** `/chat/chat-attachment/`
- **Method:** `POST`
- **Permissions:** isAuthenticated
- **Description:** Uploads a chat message with a file attachment
- **Request body:**

```json
{
  "receiver": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "message": "string",
  "attached_file": <File>
}
```

- **Responses:**

  - **201 Created**: File uploaded and chat as created successfully

  ```json
  {
    "status": "success",
    "entity": {
      "message": {
        "id": 35,
        "sender": {
          "id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437",
          "email": "onuhudoudo@gmail.com",
          "profile": null
        },
        "receiver": {
          "id": "96bf0d3f-720d-4620-8dee-0f59f997cb51",
          "email": "codebee345@outlook.com",
          "profile": null
        },
        "attached_file_size": "86.73KB",
        "message": "Hello, this is my message",
        "updated": "2024-06-17T13:14:52.773727Z",
        "created": "2024-06-17T13:14:52.773727Z",
        "seen": false,
        "deleted": false,
        "attached_file": "/mediafiles/attachments/2024/14/17/4908f104-b77b-4677-b563-b693a893fef3.jpg",
        "attached_file_name": "pexels-nappy-936119.jpg",
        "thread": 1
      }
    },
    "message": "File uploaded and chat created successfully",
    "success": true
  }
  ```

#### _Step 2: Upload send message through websocket_

utilize the id in the response from the http request above in sending the message in realtime via websocket

### Message payload: (client to server)

```json
{
  "action": "chat_message_file",
  "message_body": "hello there",
  "chat_id": "35"
}
```

#### _Step 3. Receive message from the server_

### Message response: (server to client):

Below is the realtime response that will be received by the specified receiever:

```json
{
  "message_body": "Hello, this is my message",
  "attached_file_name": "pexels-nappy-936119.jpg",
  "attached_file_size": "86.73KB",
  "attached_file_url": "/mediafiles/attachments/2024/26/17/37f67ff8-f5b8-4761-996c-04b0acf50bb9.jpg",
  "sender_id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437",
  "receiver_id": "96bf0d3f-720d-4620-8dee-0f59f997cb51",
  "timestamp": "2024-06-17T13:49:46.229768+00:00",
  "created_msg_id": 35,
  "action": "re_message_file"
}
```

- **action:** `re_message_file` Indicates that the incoming message has a file attachment.
