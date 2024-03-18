# Notification API Documentation

This documentation provides an overview of the Notification API, which is used to manage and retrieve information about notifications for users.

### Endpoints

#### 1. List Notifications for a User

- `GET /`: Retrieve a list of all notifications for the authenticated user.

##### Request

- Authentication is required.

##### Response

- Success: HTTP 200 OK with a list of all notifications for the authenticated user.
- Failure: HTTP 401 Unauthorized if the user is not authenticated.

##### Example Response

```json
[
    {
        "id": 1,
        "user": {
            "id": 1,
            "username": "user1",
            "email": "user1@example.com",
            // ... other user fields
        },
        "title": "New Message",
        "about": "You have a new message from John",
        "created": "2022-01-01T00:00:00Z",
        "seen": false
    },
    // ... more notifications
]
```

### Permissions

- `notification_list`: Requires authentication.

### CSRF Exemption

- `notification_list`: Exempted from CSRF protection.

### URL Patterns

- `/`: Maps to the `notification_list` view.

### Serializers

- `UserSerializer`: Serializes the `User` model.
- `NotificationSerializer`: Serializes the `Notification` model.

### Models

- `Notification`: Represents a notification with fields for user, title, about, created, and seen.

### Example Requests

```bash
# List all notifications for the authenticated user
curl -X GET http://myapi.nanocodes.com.ng/notifications/ -H "Authorization: Bearer <token>"
```

### Example Responses

```json
// Example response for notification_list
[
    {
        "id": 1,
        "user": {
            "id": 1,
            "username": "user1",
            "email": "user1@example.com",
            // ... other user fields
        },
        "title": "New Message",
        "about": "You have a new message from John",
        "created": "2022-01-01T00:00:00Z",
        "seen": false
    },
    // ... more notifications
]
```

