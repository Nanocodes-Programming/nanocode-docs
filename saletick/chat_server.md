# API Documentation for the websocket chat server

Api host:

```
wss://sapi.saletick.net
```

## Endpoint overview

1. **Get messages**

   - `/chat/messages/<uid>/` (GET)

2. **Get user threads**
   - `/chat/user/threads/` (GET)

# Detailed endpoint documentation

**1. Get Messages**

- **Endpoint**: `/chat/messages/<uid>/`
- **Path Parameters**:
  - `uuid` The id of the user whose conversation messages you want to fetch.
- **Description:** This endpoints gets the messages in the conversation between the currently logged-in user and the user with the uid specified in the path parameter.

- **Responses:**
  - **200 success:** Data fetched successfully

```json
{
    "status": "success",
    "entity": {
        "messages": [
            {
                "id": 1,
                "sender": {
                    "id": "b58434af-4276-47da-a0f7-0ab716168fad",
                    "email": "admin@gmail.com",
                    "username": "admin",
                    "role": null,
                    "is_active": true
                },
                "receiver": {
                    "id": "83f02f01-521c-447e-98bb-1933eba3ba09",
                    "email": "onuhudoudo@gmail.com",
                    "username": "",
                    "role": null,
                    "is_active": true
                },
                "message": "hello there, how are you",
                "updated": "2024-12-22T23:12:31.700748Z",
                "created": "2024-12-22T23:12:31.700748Z",
                "seen": false,
                "thread": 1
            },
            {
                "id": 2,
                "sender": {
                    "id": "b58434af-4276-47da-a0f7-0ab716168fad",
                    "email": "admin@gmail.com",
                    "username": "admin",
                    "role": null,
                    "is_active": true
                },
                "receiver": {
                    "id": "83f02f01-521c-447e-98bb-1933eba3ba09",
                    "email": "onuhudoudo@gmail.com",
                    "username": "",
                    "role": null,
                    "is_active": true
                },
                "message": "hello there, how are you",
                "updated": "2024-12-22T23:14:28.477068Z",
                "created": "2024-12-22T23:14:28.477068Z",
                "seen": false,
                "thread": 1
            },
            {
                "id": 3,
                "sender": {
                    "id": "b58434af-4276-47da-a0f7-0ab716168fad",
                    "email": "admin@gmail.com",
                    "username": "admin",
                    "role": null,
                    "is_active": true
                },
                "receiver": {
                    "id": "83f02f01-521c-447e-98bb-1933eba3ba09",
                    "email": "onuhudoudo@gmail.com",
                    "username": "",
                    "role": null,
                    "is_active": true
                },
                "message": "hello there, what is your name",
                "updated": "2024-12-22T23:32:06.846477Z",
                "created": "2024-12-22T23:32:06.846477Z",
                "seen": false,
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
  "message": "Invalid recipient",
  "success": false
}
```

**3. Get user threads**

- **Endpoint**: `/chat/user/threads/`
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
                "other_user": {
                    "id": "83f02f01-521c-447e-98bb-1933eba3ba09",
                    "email": "onuhudoudo@gmail.com",
                    "username": "",
                    "role": null,
                    "is_active": true
                },
                "last_message": {
                    "id": 3,
                    "sender": {
                        "id": "b58434af-4276-47da-a0f7-0ab716168fad",
                        "email": "admin@gmail.com",
                        "username": "admin",
                        "role": null,
                        "is_active": true
                    },
                    "receiver": {
                        "id": "83f02f01-521c-447e-98bb-1933eba3ba09",
                        "email": "onuhudoudo@gmail.com",
                        "username": "",
                        "role": null,
                        "is_active": true
                    },
                    "message": "hello there, what is your name",
                    "updated": "2024-12-22T23:32:06.846477Z",
                    "created": "2024-12-22T23:32:06.846477Z",
                    "seen": false,
                    "thread": 1
                }
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
- **Example url**: `wss://sapi.saletick.net/ws/chat/room/?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9haahwt`
- **Description:** Establishes a bidirectional websocket connection to the server.

Once connected to the websocket, messages can now be sent to and fro, each message carrying an action field which indicates the operation to be performed

## Sending messages

#### _Step 1. Send a message to the server_

### Message payload: (client to server)

```json
{
  "action": "chat_message",
  "message_body": "do me 2k fast",
  "receiver_id": "87c8b8e2-3efc-4a4a-b667-1f9c0d7e8437"
}
```

- **action:** "chat_message" This indicates the message is to be sent to a recipient
- **receiver_id:** The id of the user supposed to receive this message. When sent, the receiving client will receive the message immediately if they are also logged in and connected to the websocket.
- **message_body:** The text message to be sent

If the message is sent successfully, you will get a response on the senders side with a response body such as this

```json
{
    "sender_id": "a59eb80a-2820-4f01-978b-505c492a1d21",
    "receiver_id": "ab762f22-a066-4fb6-bbd0-1f774e484cba",
    "message_body": "do me 2k fast",
    "timestamp": "2024-12-23T05:25:14.763401+00:00",
    "created_msg_id": 3,
    "action": "conf_message"
}
```
- **action:** "conf_message" indicates this is a confirmation that the message you attempted to send was delivered successfully

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

- **action:** `re_message` This indicates it is a response message i.e a message is being sent to the currently connected user.
- **receiver_id:** The id of the user who is meant to receive the message
- **message_body:** The text content of the message
- **timestamp:** isoFormat time indicating when the message was sent