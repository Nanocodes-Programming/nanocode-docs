# Online Classes API Documentation

This documentation provides an overview of the Online Classes API, which is used to manage and retrieve information about online classes.

### Endpoints

#### 1. Retrieve Online Classes for a User

- `GET /`: Retrieve a list of the latest online class for each course the user is enrolled in.

##### Request

- Authentication is required.

##### Response

- Success: HTTP 200 OK with a list of the latest online class for each course the user is enrolled in.
- Failure: HTTP 401 Unauthorized if the user is not authenticated.

##### Example Response

```json
[
    {
        "id": 1,
        "course": "Course Title",
        "link": "https://example.com/class",
        "starts": "2022-01-01T00:00:00Z",
        "ends": "2022-01-01T01:00:00Z"
    },
    // ... more classes
]
```

#### 2. Create an Online Class

- `POST /create`: Create a new online class.

##### Request

- Authentication is required.
- Body:
  - `course`: The title of the course.
  - `link`: The URL of the online class.
  - `starts`: The start time of the online class.
  - `ends`: The end time of the online class.

##### Response

- Success: HTTP 200 OK with the details of the created online class.
- Failure: HTTP 400 Bad Request with error message if the course does not exist.

##### Example Response

```json
{
    "course": "Course Title",
    "link": "https://example.com/class",
    "starts": "2022-01-01T00:00:00Z",
    "ends": "2022-01-01T01:00:00Z"
}
```

### Permissions

- `onlineclass_detail`: Requires authentication.
- `onlineclass_create`: Requires authentication.

### URL Patterns

- `/`: Maps to the `onlineclass_detail` view.
- `/create`: Maps to the `onlineclass_create` view.

### Serializer

- `OnlineClassCreateSerializer`: Serializes the `OnlineClass` model for creation.

### Model

- `OnlineClass`: Represents an online class with fields for course, link, starts, and ends.

### Example Requests

```bash
# Retrieve online classes for a user
curl -X GET http://myapi.nanocodes.com.ng/onlineclass/ -H "Authorization: Bearer <token>"

# Create a new online class
curl -X POST http://myapi.nanocodes.com.ng/onlineclass/create -H "Authorization: Bearer <token>" -d '{"course": "Course Title", "link": "https://example.com/class", "starts": "2022-01-01T00:00:00Z", "ends": "2022-01-01T01:00:00Z"}'
```

### Example Responses

```json
// Example response for onlineclass_detail
[
    {
        "id": 1,
        "course": "Course Title",
        "link": "https://example.com/class",
        "starts": "2022-01-01T00:00:00Z",
        "ends": "2022-01-01T01:00:00Z"
    },
    // ... more classes
]

// Example response for onlineclass_create
{
    "course": "Course Title",
    "link": "https://example.com/class",
    "starts": "2022-01-01T00:00:00Z",
    "ends": "2022-01-01T01:00:00Z"
}
```

### Notes

- The `onlineclass_detail` view retrieves the latest online class for each course the authenticated user is enrolled in.
- The `onlineclass_create` view creates a new online class for a course. The course title is used to look up the `Course` object.
- The `raise_exception=True` parameter in `serializer.is_valid()` will automatically return a 400 response with the validation errors if the data is not valid.
- The `@csrf_exempt` decorator is used to allow POST requests from other domains, which is generally not recommended due to security reasons. If you need to allow cross-domain requests, consider using Django's CORS settings or a third-party package like `django-cors-headers`.

Remember to replace `<token>` in the `Authorization: Bearer <token>` header with a valid JWT token for the `onlineclass_detail` and `onlineclass_create` endpoints.
