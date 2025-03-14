# API Documentation for the websocket chat server

Api host:

```
wss://licomed.up.railway.app
```

## Endpoint overview

1. **Get messages**

   - `/chat/messages/<uid>/` (GET)

2. **Upload chat with an attachment**

   - `/chat/attachment/` (POST)

3. **Get user threads**

   - `/chat/user/threads/` (GET)

4. **Get files in a thread**
   - `/chat/thread/files/<thread_id>/` (GET)

# Detailed endpoint documentation

- **Endpoint**: `/chat/messages/<uid>/`
- **Path Parameters**:
  - `uuid` The id of the user whose conversation messages you want to create.
- **Description:** This endpoints gets the messages in the conversation between the currently logged-in user and the user with the uid specified in the path parameter.

- **Responses:**
  - **200 success:** Data fetched successfully

```json
{
  "status": "success",
  "data": {
    "messages": [
      {
        "id": 3,
        "sender": {
          "id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
          "password": "pbkdf2_sha256$870000$odJsycXTQvPMavecYznziC$ClTC71hFKe3twI8mKycYqhNwW5iXd6gVZXWrW+y88wQ=",
          "last_login": null,
          "gender": "male",
          "email": "onuhudoudo@gmail.com",
          "fullname": "Kyrian developer",
          "country_code": "+234",
          "phone_number": "9128168542",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": false,
          "is_admin": false,
          "is_superuser": false,
          "created_at": "2025-03-06T12:10:08.694946Z",
          "updated_at": "2025-03-14T09:31:21.194855Z",
          "account_type": "user",
          "date_of_birth": "2025-03-06",
          "profile_photo": null,
          "is_profile_complete": true,
          "groups": [],
          "user_permissions": []
        },
        "receiver": {
          "id": "75140d72-8b20-4549-885c-20599badb486",
          "password": "pbkdf2_sha256$870000$OJK2qo1SwDjArqY480uPeK$SMtMfGho+yIukvvsPjSezOggvVuBoH8jvC3egfFAbqs=",
          "last_login": "2025-03-14T09:43:53.882070Z",
          "gender": "male",
          "email": "admin@gmail.com",
          "fullname": "Admin user",
          "country_code": "",
          "phone_number": "admin",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": true,
          "is_admin": true,
          "is_superuser": true,
          "created_at": "2025-03-06T10:15:38.986890Z",
          "updated_at": "2025-03-14T09:44:20.920766Z",
          "account_type": "user",
          "date_of_birth": "2025-03-14",
          "profile_photo": null,
          "is_profile_complete": false,
          "groups": [],
          "user_permissions": []
        },
        "attached_file_size": "194.75KB",
        "message": "",
        "updated_at": "2025-03-14T10:07:31.270646Z",
        "created_at": "2025-03-14T10:07:31.270661Z",
        "attached_file": "/media/chat-files/Screenshot_2025-03-14_100311.png",
        "message_type": "file",
        "attached_file_name": "bitcoin",
        "thread": 1,
        "attached_profile": null
      },
      {
        "id": 2,
        "sender": {
          "id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
          "password": "pbkdf2_sha256$870000$odJsycXTQvPMavecYznziC$ClTC71hFKe3twI8mKycYqhNwW5iXd6gVZXWrW+y88wQ=",
          "last_login": null,
          "gender": "male",
          "email": "onuhudoudo@gmail.com",
          "fullname": "Kyrian developer",
          "country_code": "+234",
          "phone_number": "9128168542",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": false,
          "is_admin": false,
          "is_superuser": false,
          "created_at": "2025-03-06T12:10:08.694946Z",
          "updated_at": "2025-03-14T09:31:21.194855Z",
          "account_type": "user",
          "date_of_birth": "2025-03-06",
          "profile_photo": null,
          "is_profile_complete": true,
          "groups": [],
          "user_permissions": []
        },
        "receiver": {
          "id": "75140d72-8b20-4549-885c-20599badb486",
          "password": "pbkdf2_sha256$870000$OJK2qo1SwDjArqY480uPeK$SMtMfGho+yIukvvsPjSezOggvVuBoH8jvC3egfFAbqs=",
          "last_login": "2025-03-14T09:43:53.882070Z",
          "gender": "male",
          "email": "admin@gmail.com",
          "fullname": "Admin user",
          "country_code": "",
          "phone_number": "admin",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": true,
          "is_admin": true,
          "is_superuser": true,
          "created_at": "2025-03-06T10:15:38.986890Z",
          "updated_at": "2025-03-14T09:44:20.920766Z",
          "account_type": "user",
          "date_of_birth": "2025-03-14",
          "profile_photo": null,
          "is_profile_complete": false,
          "groups": [],
          "user_permissions": []
        },
        "attached_file_size": "0kb",
        "message": null,
        "updated_at": "2025-03-14T09:52:23.143598Z",
        "created_at": "2025-03-14T09:52:23.143613Z",
        "attached_file": null,
        "message_type": "user_profile",
        "attached_file_name": null,
        "thread": 1,
        "attached_profile": "75140d72-8b20-4549-885c-20599badb486"
      },
      {
        "id": 1,
        "sender": {
          "id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
          "password": "pbkdf2_sha256$870000$odJsycXTQvPMavecYznziC$ClTC71hFKe3twI8mKycYqhNwW5iXd6gVZXWrW+y88wQ=",
          "last_login": null,
          "gender": "male",
          "email": "onuhudoudo@gmail.com",
          "fullname": "Kyrian developer",
          "country_code": "+234",
          "phone_number": "9128168542",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": false,
          "is_admin": false,
          "is_superuser": false,
          "created_at": "2025-03-06T12:10:08.694946Z",
          "updated_at": "2025-03-14T09:31:21.194855Z",
          "account_type": "user",
          "date_of_birth": "2025-03-06",
          "profile_photo": null,
          "is_profile_complete": true,
          "groups": [],
          "user_permissions": []
        },
        "receiver": {
          "id": "75140d72-8b20-4549-885c-20599badb486",
          "password": "pbkdf2_sha256$870000$OJK2qo1SwDjArqY480uPeK$SMtMfGho+yIukvvsPjSezOggvVuBoH8jvC3egfFAbqs=",
          "last_login": "2025-03-14T09:43:53.882070Z",
          "gender": "male",
          "email": "admin@gmail.com",
          "fullname": "Admin user",
          "country_code": "",
          "phone_number": "admin",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": true,
          "is_admin": true,
          "is_superuser": true,
          "created_at": "2025-03-06T10:15:38.986890Z",
          "updated_at": "2025-03-14T09:44:20.920766Z",
          "account_type": "user",
          "date_of_birth": "2025-03-14",
          "profile_photo": null,
          "is_profile_complete": false,
          "groups": [],
          "user_permissions": []
        },
        "attached_file_size": "0kb",
        "message": null,
        "updated_at": "2025-03-14T09:50:22.310601Z",
        "created_at": "2025-03-14T09:50:22.310616Z",
        "attached_file": null,
        "message_type": "user_profile",
        "attached_file_name": null,
        "thread": 1,
        "attached_profile": "75140d72-8b20-4549-885c-20599badb486"
      }
    ]
  },
  "message": "Messages retrieved successfully",
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

- **Endpoint**: `/chat/user/threads/`
- **Permissions:** isAuthenticated
- **Description:** Gets the threads associated with the currently logged-in user. A thread basically respresents a conversation between two users.

```json
{
  "status": "success",
  "data": [
    {
      "id": 1,
      "other_user": {
        "id": "75140d72-8b20-4549-885c-20599badb486",
        "password": "pbkdf2_sha256$870000$OJK2qo1SwDjArqY480uPeK$SMtMfGho+yIukvvsPjSezOggvVuBoH8jvC3egfFAbqs=",
        "last_login": "2025-03-14T09:43:53.882070Z",
        "gender": "male",
        "email": "admin@gmail.com",
        "fullname": "Admin user",
        "country_code": "",
        "phone_number": "admin",
        "is_email_verified": true,
        "is_phone_verified": true,
        "is_active": true,
        "is_staff": true,
        "is_admin": true,
        "is_superuser": true,
        "created_at": "2025-03-06T10:15:38.986890Z",
        "updated_at": "2025-03-14T09:44:20.920766Z",
        "account_type": "user",
        "date_of_birth": "2025-03-14",
        "profile_photo": null,
        "is_profile_complete": false,
        "groups": [],
        "user_permissions": []
      },
      "last_message": {
        "id": 1,
        "sender": {
          "id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
          "password": "pbkdf2_sha256$870000$odJsycXTQvPMavecYznziC$ClTC71hFKe3twI8mKycYqhNwW5iXd6gVZXWrW+y88wQ=",
          "last_login": null,
          "gender": "male",
          "email": "onuhudoudo@gmail.com",
          "fullname": "Kyrian developer",
          "country_code": "+234",
          "phone_number": "9128168542",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": false,
          "is_admin": false,
          "is_superuser": false,
          "created_at": "2025-03-06T12:10:08.694946Z",
          "updated_at": "2025-03-14T09:31:21.194855Z",
          "account_type": "user",
          "date_of_birth": "2025-03-06",
          "profile_photo": null,
          "is_profile_complete": true,
          "groups": [],
          "user_permissions": []
        },
        "receiver": {
          "id": "75140d72-8b20-4549-885c-20599badb486",
          "password": "pbkdf2_sha256$870000$OJK2qo1SwDjArqY480uPeK$SMtMfGho+yIukvvsPjSezOggvVuBoH8jvC3egfFAbqs=",
          "last_login": "2025-03-14T09:43:53.882070Z",
          "gender": "male",
          "email": "admin@gmail.com",
          "fullname": "Admin user",
          "country_code": "",
          "phone_number": "admin",
          "is_email_verified": true,
          "is_phone_verified": true,
          "is_active": true,
          "is_staff": true,
          "is_admin": true,
          "is_superuser": true,
          "created_at": "2025-03-06T10:15:38.986890Z",
          "updated_at": "2025-03-14T09:44:20.920766Z",
          "account_type": "user",
          "date_of_birth": "2025-03-14",
          "profile_photo": null,
          "is_profile_complete": false,
          "groups": [],
          "user_permissions": []
        },
        "attached_file_size": "0kb",
        "message": null,
        "updated_at": "2025-03-14T09:50:22.310601Z",
        "created_at": "2025-03-14T09:50:22.310616Z",
        "attached_file": null,
        "message_type": "user_profile",
        "attached_file_name": null,
        "thread": 1,
        "attached_profile": "75140d72-8b20-4549-885c-20599badb486"
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
- **Example url**: `wss://host.com/ws/chat/room/?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`
- **Description:** Establishes a bidirectional websocket connection to the server.

Once connected to the websocket, messages can now be sent to and fro, each message carrying an action field which indicates the operation to be performed

There a three types of chat messages

1. text
2. user_profile
3. file

## Sending plain text messages

#### _Step 1. Send a message to the server_

### Message payload: (client to server)

```json
{
  "action": "text_message",
  "message_body": "hello there",
  "receiver_id": "75140d72-8b20-4549-885c-20599badb486"
}
```

- **action:** "text_message" This indicates the message is just a regular text message
- **receiver_id:** The id of the user supposed to receive this message. When sent, the receiving client will receive the message immediately if they are also logged in and connected to the websocket.
- **message_body:** The text message to be sent

\*\*Note: the message that was sent also bounces back to the sender as a confirmation

#### _Step 2. Receive message from the server_

### Message response: (server to client):

When a message with the action of `text_message` is sent, the server stores the message in the database and deliveres it in real time to the user with the specified `receiver_id`, it also bounces the message that was sent back to the sender

Below is the realtime response that will be received by the specified receiever:

```json
{
  "sender_id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
  "receiver_id": "75140d72-8b20-4549-885c-20599badb486",
  "message": "hello there",
  "timestamp": "2025-03-14T10:36:22.680911+00:00",
  "created_msg_id": 4,
  "message_type": "text",
  "action": "re_message"
}
```

Below is the response that bounces back to the sender

```json
{
  "sender_id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
  "receiver_id": "75140d72-8b20-4549-885c-20599badb486",
  "message": "hello there",
  "timestamp": "2025-03-14T10:36:22.680911+00:00",
  "created_msg_id": 4,
  "message_type": "text",
  "action": "conf_message"
}
```

- **action:** `re_message` This indicates it is a response message.
- **action:** `conf_message` This indicates it is a confirmation message.
- **receiver_id:** The id of the user who is meant to receive the message
- **message_body:** The text content of the message
- **timestamp:** isoFormat time indicating when the message was sent

## Sending messages with a file attachment

Due to the fact that transfering files through a websocket endpoint can be overly resource intensive, it is required to upload files to a http endpoint after which the chat message is sent via websocket.

#### _Step 1: Upload chat and file to server using http endpoint_

- **Endpoint:** `/chat/attachment/`
- **Method:** `POST`
- **Permissions:** isAuthenticated
- **Description:** Uploads a chat message with a file attachment
- **Request body:**

```json
{
  "receiver": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "message": "string",
  "attached_file": <File>,
  "attached_file_name": "string"
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
  "action": "file_message",
  "chat_id": 5
}
```

#### _Step 3. Receive message from the server_

Below is the realtime response that will be received by the specified receiever:

```json
{
  "message_body": "this is the file",
  "attached_file_name": "Screenshot 2025-03-14 100311.png",
  "attached_file_size": "194.75KB",
  "sender_id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
  "receiver_id": "75140d72-8b20-4549-885c-20599badb486",
  "timestamp": "2025-03-14T10:45:51.147140+00:00",
  "created_msg_id": 5,
  "action": "re_message",
  "message_type": "file"
}
```

Below is the realtime response that will be bounced back to the sender

```json
{
  "message_body": "this is the file",
  "attached_file_name": "Screenshot 2025-03-14 100311.png",
  "attached_file_size": "194.75KB",
  "sender_id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
  "receiver_id": "75140d72-8b20-4549-885c-20599badb486",
  "timestamp": "2025-03-14T10:45:51.147140+00:00",
  "created_msg_id": 5,
  "action": "conf_message",
  "message_type": "file"
}
```

- **action:** `re_message` This indicates it is a response message.
- **action:** `conf_message` This indicates it is a confirmation message.
- **type:** `file` This indicates that the message is a file messagee.

## Sending messages with a profile attachment

#### _Step 1. Send a message to the server_

### Message payload: (client to server)

```json
{
  "attached_profile_id": "75140d72-8b20-4549-885c-20599badb486",
  "receiver_id": "75140d72-8b20-4549-885c-20599badb486",
  "action": "user_profile_message"
}
```

- **action:** "user_profile_message" This indicates the message is a user_profile_attachment, it does not carry a file
- **receiver_id:** The id of the user supposed to receive this message. When sent, the receiving client will receive the message immediately if they are also logged in and connected to the websocket.
- **attached_profile_id:** The user id of the profile that is to be attached

#### _Step 2. Receive message from the server_

### Message response: (server to client):

Below is the realtime response that will be received by the specified receiever:

```json
{
    "sender_id": "302e305b-6e73-4f9c-bac7-551a92b106b0",
    "receiver_id": "75140d72-8b20-4549-885c-20599badb486",
    "message": null,
    "timestamp": "2025-03-14T10:52:54.603043+00:00",
    "created_msg_id": 6,
    "attached_profile": {
        "id": "75140d72-8b20-4549-885c-20599badb486",
        "fullname": "Admin user",
        "phone_number": "admin"
    },
    "message_type": "user_profile",
    "action": "re_message"
}
```

This response is also bounced back to the sender, The action type of the message that is bounced back to the sender will be `conf_message`

- **action:** `re_message` This indicates it is a response message.
- **action:** `conf_message` This indicates it is a confirmation message.
- **type:** `user_profile` This indicates that the message is a user_profile.

