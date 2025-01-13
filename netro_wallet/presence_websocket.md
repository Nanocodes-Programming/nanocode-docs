# Documentation for the presence websocket

Api host:

```
wss://api.netroxchange.com/
```

The user object contains a field called `is_online`, this will be used to initially display the users online status but changes in the online status of the user will be propagated through the websocket


## **Connecting and using the websocket**

- **Endpoint**: `/ws/presence/`
- **Query Parameters**:
  - `?token=` This is the access token of the currently logged in user.
- **Example url**: `wss://host.com/ws/presence/?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`
- **Description:** Establishes a bidirectional websocket connection to the server and marks the user as online.


When a user connects to the WebSocket, all other connected users are notified that the new user is now online. Each connected user will receive a message in the following format:

```json
{
    "action": "presence",
    "status": "online",
    "user_id": "a0f4b68d-90b9-4aaf-82e5-4c500f702fb1"
}
```

Also when a user disconnects from the websocket, every other connected user receives a message in the following format

```json
{
    "action": "presence",
    "status": "offline",
    "user_id": "598b1f02-b6b5-4197-a399-c8537e45d768"
}
```

Notice the status of a connected user is `online` and the status of a disconnected user is `offline`

