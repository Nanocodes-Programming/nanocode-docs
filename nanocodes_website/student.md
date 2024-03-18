# Student Count API Documentation

This documentation provides an overview of the Student Count API, which is used to retrieve the total number of students in the system.

### Endpoint

- `GET /api/students/count/`: Retrieve the total number of students.

### Request

- No parameters are required for this endpoint.

### Response

- Success: HTTP 200 OK with the total number of students.
- Failure: HTTP 400 Bad Request with error message.

### Example Response

```json
{
    "count": 500
}
```

### Description

The Student Count API endpoint is used to retrieve the total number of students in the system. This is useful for tracking the growth of the student base or for displaying statistics related to students.

### Permissions

This endpoint does not require authentication. Anyone can access it.

### CSRF Exemption

This endpoint is exempted from CSRF protection. This means that it can be accessed from any source, including other domains.

### URL Pattern

The URL pattern for this endpoint is `/api/students/count/`.

### View Function

The view function for this endpoint is `user_count`, which is defined in the `views.py` file.

### Serializer

The `UserCountSerializer` is used to serialize the student count data. It has a `get_count` method that returns the total number of students.

### Note

The get_count method in the UserCountSerializer is used to count the number of students in the system. It filters the User model for users where is_student is True and then counts the number of such users.

### Example Request

```bash
curl -X GET http://myapi.nanocodes.com.ng/students/user-count/
```

### Example Response

```json
{
    "count": 500
}
```

This response indicates that there are 500 students in the system.