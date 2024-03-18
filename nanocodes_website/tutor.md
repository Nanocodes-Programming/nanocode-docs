# Tutor API Documentation

This documentation provides an overview of the Tutor API, which is used to manage and retrieve information about tutors.

### Endpoints

#### 1. List Tutors

- `GET /`: Retrieve a list of all tutors.

##### Request

- No parameters are required for this endpoint.

##### Response

- Success: HTTP 200 OK with a list of all tutors.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
[
    {
        "id": 1,
        "name": "John Doe",
        "email": "john.doe@example.com",
        "image": "http://example.com/image.jpg",
        "description": "I am a math tutor",
        "role": "Math Tutor",
        "github_link": "http://github.com/johndoe"
    },
    // ... more tutors
]
```

#### 2. Retrieve Tutor Details

- `GET /{id}`: Retrieve details of a specific tutor.

##### Request

- `id`: The ID of the tutor.

##### Response

- Success: HTTP 200 OK with the details of the specified tutor.
- Failure: HTTP 404 Not Found if the tutor does not exist.

##### Example Response

```json
{
    "id": 1,
    "name": "John Doe",
    "email": "john.doe@example.com",
    "image": "http://example.com/image.jpg",
    "description": "I am a math tutor",
    "role": "Math Tutor",
    "github_link": "http://github.com/johndoe"
}
```

#### 3. Get Students by Tutor

- `GET /get_students_by_tutor/{tutor_id}`: Retrieve a list of students taught by a specific tutor.

##### Request

- `tutor_id`: The ID of the tutor.

##### Response

- Success: HTTP 200 OK with a list of students taught by the specified tutor.
- Failure: HTTP 404 Not Found if the tutor does not exist.

##### Example Response

```json
[
    {
        "id": 1,
        "username": "student1",
        "email": "student1@example.com",
        // ... other user fields
    },
    // ... more students
]
```

#### 4. Get Students by Tutor and Tag

- `GET /get_students_by_tutor_and_tag/{tutor_id}/{tag_id}`: Retrieve a list of students taught by a specific tutor and enrolled in a specific tag.

##### Request

- `tutor_id`: The ID of the tutor.
- `tag_id`: The ID of the tag.

##### Response

- Success: HTTP 200 OK with a list of students taught by the specified tutor and enrolled in the specified tag.
- Failure: HTTP 404 Not Found if the tutor or tag does not exist.

##### Example Response

```json
[
    {
        "id": 1,
        "username": "student1",
        "email": "student1@example.com",
        // ... other user fields
    },
    // ... more students
]
```

### Permissions

- `tutor_list`: Allows anyone to access.
- `tutor_detail`: Allows anyone to access.
- `GetStudentsByTutorsViewSet`: Requires authentication.
- `GetStudentsByTutorAndTagViewSet`: Requires authentication.

### CSRF Exemption

- `tutor_list`: Exempted from CSRF protection.
- `tutor_detail`: Exempted from CSRF protection.
- `GetStudentsByTutorsViewSet`: Exempted from CSRF protection.
- `GetStudentsByTutorAndTagViewSet`: Exempted from CSRF protection.

### URL Patterns

- `/`: Maps to the `tutor_list` view.
- `/{id}`: Maps to the `tutor_detail` view.
- `/get_students_by_tutor/{tutor_id}`: Maps to the `GetStudentsByTutorsViewSet` view.
- `/get_students_by_tutor_and_tag/{tutor_id}/{tag_id}`: Maps to the `GetStudentsByTutorAndTagViewSet` view.

### Serializers

- `TutorSerializer`: Serializes the `Tutor` model.

### Models

- `Tutor`: Represents a tutor with fields for name, email, image, description, role, and GitHub link.

### Example Requests

```bash
# List all tutors
curl -X GET http://myapi.nanocodes.com.ng/tutors/

# Retrieve details of a specific tutor
curl -X GET http://myapi.nanocodes.com.ng/tutors/1

# Get students by tutor
curl -X GET http://myapi.nanocodes.com.ng/tutors/get_students_by_tutor/1

# Get students by tutor and tag
curl -X GET http://myapi.nanocodes.com.ng/tutors/get_students_by_tutor_and_tag/1/1
```

### Example Responses

```json
// Example response for tutor_list
[
    {
        "id": 1,
        "name": "John Doe",
        "email": "john.doe@example.com",
        "image": "http://example.com/image.jpg",
        "description": "I am a math tutor",
        "role": "Math Tutor",
        "github_link": "http://github.com/johndoe"
    },
    // ... more tutors
]

// Example response for tutor_detail
{
    "id": 1,
    "name": "John Doe",
    "email": "john.doe@example.com",
    "image": "http://example.com/image.jpg",
    "description": "I am a math tutor",
    "role": "Math Tutor",
    "github_link": "http://github.com/johndoe"
}

// Example response for GetStudentsByTutorsViewSet and GetStudentsByTutorAndTagViewSet
[
    {
        "id": 1,
        "username": "student1",
        "email": "student1@example.com",
        // ... other user fields
    },
    // ... more students
]
```