# API Documentation for the websocket chat server

Api host for websocket: 
```
wss://api.9app.co
```


## Endpoint overview
1. **Get messages**
    - `/chat/messages/<uid>/` (GET)

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
            },
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
                "id": "8b979f92-2d5d-471f-abdc-4f8259f5736a",
                "email": "udokyrian@outlook.com",
                "first_name": "Onuh",
                "last_name": "Udochukwu"
            },
            "user_two": {
                "id": "68f6cebe-1dfb-418d-8c4e-3ada680984d1",
                "email": "onuhudoudo@gmail.com",
                "first_name": "udo",
                "last_name": "onuh"
            },
            "last_message": "hello there, how are you",
            "craeted": "2024-08-01T15:56:02.183570Z"
        }
    ],
    "message": null,
    "success": true
    }
    ```

## **Connecting and using the websocket**
- **Endpoint**: `/chat/room/ws/`
- **Query Parameters**: 
    - `?token=` This is the access token of the currently logged in user.
- **Example url**: `wss://host.com/ws/chat/room/?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`
- **Description:** Establishes a bidirectional websocket connection to the server. 

Once connected to the websocket, messages can now be sent to and fro, each message carrying an action field which indicates the operation to be performed 

## Sending messages

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

# HTTP ENDOPINTS 

## Get all users 

```
/auth/users/
```
**Method:** `POST`  
**Permissions:** IsAuthenticated 

### Sample response 
```json
{
    "status": "success",
    "entity": [
        {
            "id": "68f6cebe-1dfb-418d-8c4e-3ada680984d1",
            "password": "pbkdf2_sha256$600000$oH9ngp1WKImQge2X5v8jxT$qGxwp2CQfnuKeowhi/kxb3MqYlcaXV1zL33uvuMY9tg=",
            "last_login": "2024-08-01T15:52:39Z",
            "email": "onuhudoudo@gmail.com",
            "first_name": "udo",
            "last_name": "onuh",
            "phone_number": "08143015512",
            "email_verified": false,
            "phone_number_verified": true,
            "is_staff": true,
            "is_superuser": true,
            "is_active": true,
            "has_kyc": false,
            "two_factor_enabled": false,
            "two_factor_type": "email",
            "available_balance": "0.00000",
            "user_number": 1,
            "created_at": "2024-07-25T14:23:43.103338Z",
            "country": null,
            "updated_at": "2024-08-09T19:18:24.031688Z",
            "groups": [],
            "user_permissions": []
        },
        {
            "id": "8b979f92-2d5d-471f-abdc-4f8259f5736a",
            "password": "pbkdf2_sha256$600000$r4tQDYE9WGWsznm5KajcJf$nC5XrNeefJHVDIm/Gbj5OTqrrYpod5YhhMmZF/XuEWI=",
            "last_login": null,
            "email": "udokyrian@outlook.com",
            "first_name": "Onuh",
            "last_name": "Udochukwu",
            "phone_number": "09128168542",
            "email_verified": true,
            "phone_number_verified": true,
            "is_staff": true,
            "is_superuser": false,
            "is_active": true,
            "has_kyc": false,
            "two_factor_enabled": false,
            "two_factor_type": "email",
            "available_balance": "0.00000",
            "user_number": 2,
            "created_at": "2024-08-01T15:54:34.514990Z",
            "country": null,
            "updated_at": "2024-08-01T15:54:34.514990Z",
            "groups": [],
            "user_permissions": []
        }
    ],
    "message": null,
    "success": true
}
```


## Enable a coin

```
/exec/coin/enable/
```
**Method:** `GET`  
**Permissions:** IsAuthenticated

### Request body 
```json
    {
        "coin": "string"
    }
```

### Responses 
```json
{
    "status": "success",
    "entity": null,
    "message": "btc enabled successfully",
    "success": true
}
```
200. Coin was enabled 

```json
{
    "status": "failure",
    "entity": null,
    "message": "Invalid coin",
    "success": false
}
```
404. Coin is not supported



## Disable a coin 

```
/exec/coin/disable/
```
**Method:** `GET`  
**Permissions:** IsAuthenticated

### Request body 
```json
    {
        "coin": "string"
    }
```

### Responses 
```json
{
    "status": "success",
    "entity": null,
    "message": "btc disabled successfully",
    "success": true
}
```
200. Coin was disabled 

```json
{
    "status": "failure",
    "entity": null,
    "message": "Invalid coin",
    "success": false
}
```
404. Coin is not supported


## Get a list of all transactions  

```
{{base_url}}/transactions/all/
```
**Method:** `GET`  
**Permissions:** IsAuthenticated


### Responses 
```json
[
    {
        "id": "5b9ae820-dc6a-482e-87e6-9d5b9827cb4f",
        "user": {
            "id": "8b979f92-2d5d-471f-abdc-4f8259f5736a",
            "email": "udokyrian@outlook.com",
            "first_name": "Onuh",
            "last_name": "Udochukwu",
            "phone_number": "09128168542",
            "has_kyc": false,
            "two_factor_enabled": false,
            "two_factor_type": "email"
        },
        "amount": "50.00000",
        "transaction_type": "DEPOSIT",
        "status": "PENDING",
        "created": "2024-08-01T16:24:34.950837Z"
    }
]
```
200. successful


## Get a list of all deposits  

```
{{base_url}}/deposits/list/all/
```
**Method:** `GET`  
**Permissions:** IsAuthenticated


### Responses 
```json
[
    {
        "id": "329a18d6-b692-4e72-9d81-293e819b49ff",
        "user": {
            "id": "68f6cebe-1dfb-418d-8c4e-3ada680984d1",
            "email": "onuhudoudo@gmail.com",
            "first_name": "udo",
            "last_name": "onuh",
            "phone_number": "08143015512",
            "has_kyc": false,
            "two_factor_enabled": false,
            "two_factor_type": "email"
        },
        "created": "2024-08-01T16:47:33.478557Z",
        "updated_at": "2024-08-01T16:47:33.478557Z",
        "amount": "50.00000",
        "wallet_type": "BTC",
        "wallet_address": "jdjfj9435",
        "naira_amount": "90000.00000",
        "verified": true
    }
]
```
200. successful


## Get a list of all withdrawals  

```
{{base_url}}/withdrawals/list/all/
```
**Method:** `GET`  
**Permissions:** IsAuthenticated


### Responses 
```json
[
    {
        "id": "42a02848-e6bf-412b-a5c4-afe434a2b09e",
        "created": "2024-08-04T21:57:39.784998Z",
        "amount": "500.00000",
        "wallet_type": "BTC",
        "wallet_address": "7d39dl9039x9o3kfb",
        "naira_amount": "7000000.00000",
        "verified": true,
        "wallet_type_display": "Bitcoin"
    },
    {
        "id": "26659604-fc09-4af6-88ef-2eab856fd9cd",
        "created": "2024-08-01T16:58:47.132822Z",
        "amount": "6.00000",
        "wallet_type": "BTC",
        "wallet_address": "irkek9393krrk94i4je33d",
        "naira_amount": "600.00000",
        "verified": true,
        "wallet_type_display": "Bitcoin"
    }
]
```
200. successful

## Get user settings 

```
{{base_url}}/exec/user/settings/{{user_id}}/
```
**Method:** `GET`  
**Permissions:** IsAuthenticated


### Responses 
```json
{
    "status": "success",
    "entity": {
        "user": {
            "id": "68f6cebe-1dfb-418d-8c4e-3ada680984d1",
            "email": "onuhudoudo@gmail.com",
            "first_name": "udo",
            "last_name": "onuh",
            "phone_number": "08143015512",
            "has_kyc": false,
            "two_factor_enabled": false,
            "two_factor_type": "email"
        },
        "is_active": true,
        "can_trade_btc": false,
        "can_trade_ltc": true,
        "can_trade_usdt": true,
        "can_trade_bnb": true,
        "can_trade_eth": true
    },
    "message": null,
    "success": true
}
```
200. successful


## Change user settings 

```
{{base_url}}/exec/user/settings/{{user_id}}/
```
**Method:** `GET`  
**Permissions:** IsAuthenticated

### Request body

```json 
{
  "is_active": true,
  "can_trade_btc": true,
  "can_trade_usdt": true,
  "can_trade_bnb": true,
  "can_trade_eth": true,
  "can_trade_ltc": true,
  "can_withdraw": true,
  "can_deposit": true,
  "can_transfer": true
}
```

### Responses 
```json
{
    "status": "success",
    "entity": {
        "user": {
            "id": "68f6cebe-1dfb-418d-8c4e-3ada680984d1",
            "email": "onuhudoudo@gmail.com",
            "first_name": "udo",
            "last_name": "onuh",
            "phone_number": "08143015512",
            "has_kyc": false,
            "two_factor_enabled": false,
            "two_factor_type": "email"
        },
        "is_active": true,
        "can_trade_btc": true,
        "can_trade_ltc": true,
        "can_trade_usdt": true,
        "can_trade_bnb": true,
        "can_trade_eth": true
    },
    "message": "User settings updated successfully",
    "success": true
}
```
200. successful











