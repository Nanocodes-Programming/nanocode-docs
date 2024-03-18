# Timetable API Documentation

This documentation provides an overview of the Timetable API, which is used to manage and retrieve timetable information for students and tutors.

### Endpoints

#### 1. Get Timetable for a User

- `GET /`: Retrieve the timetable for the authenticated user.

##### Request

- No parameters are required for this endpoint.

##### Response

- Success: HTTP 200 OK with the user's timetable.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
[
    {
        "id": 1,
        "course": {
            "id": 1,
            "course_title": "Math",
            "course_description": "Mathematics for beginners",
            "tutor": {
                "id": 1,
                "user": 1,
                "bio": "I am a math tutor",
                "profile_picture": "http://example.com/image.jpg"
            }
        },
        "day": "monday",
        "starts": "09:00:00",
        "ends": "10:30:00"
    },
    // ... more classes
]
```

#### 2. Get Timetable by Day

- `GET /get_timetable_by_day/{day}`: Retrieve the timetable for the authenticated user on a specific day.

##### Request

- `day`: The day of the week for which to retrieve the timetable.

##### Response

- Success: HTTP 200 OK with the user's timetable for the specified day.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
[
    {
        "id": 1,
        "course": {
            "id": 1,
            "course_title": "Math",
            "course_description": "Mathematics for beginners",
            "tutor": {
                "id": 1,
                "user": 1,
                "bio": "I am a math tutor",
                "profile_picture": "http://example.com/image.jpg"
            }
        },
        "day": "monday",
        "starts": "09:00:00",
        "ends": "10:30:00"
    },
    // ... more classes
]
```

#### 3. Create a Timetable Entry

- `POST /create`: Create a new timetable entry for a course.

##### Request

- `course`: The title of the course.
- `starts`: The start time of the class.
- `ends`: The end time of the class.
- `day`: The day of the week for the class.
- `category`: The category of the class (e.g., "alpha", "sigma").

##### Response

- Success: HTTP 200 OK with the created timetable entry.
- Failure: HTTP 400 Bad Request with error message.

##### Example Request

```json
{
    "course": "Math",
    "starts": "09:00:00",
    "ends": "10:30:00",
    "day": "monday",
    "category": "alpha"
}
```

##### Example Response

```json
{
    "course": "Math",
    "starts": "09:00:00",
    "ends": "10:30:00",
    "day": "monday",
    "category": "alpha"
}
```

### Permissions

- `timetable_detail`: Requires authentication.
- `get_timetable_by_days`: Requires authentication.
- `timetable_create`: Requires authentication and the user must be a tutor or read-only.

### CSRF Exemption

- `timetable_detail`: Exempted from CSRF protection.
- `get_timetable_by_days`: Exempted from CSRF protection.
- `timetable_create`: Exempted from CSRF protection.

### URL Patterns

- `/`: Maps to the `timetable_detail` view.
- `/get_timetable_by_day/{day}`: Maps to the `get_timetable_by_days` view.
- `/create`: Maps to the `timetable_create` view.

### Serializers

- `TimeTableSerializer`: Serializes the `TimeTable` model.
- `TimeTableCreateSerializer`: Serializes the data for creating a new `TimeTable` entry.

### Models

- `TimeTable`: Represents a timetable entry for a course.

### Note

The `TimeTable` model has a foreign key relationship with the `Course` model, which in turn has a foreign key relationship with the `Tutor` model. The `TimeTableSerializer` includes nested serialization for the `Course` and `Tutor` models to provide more detailed information about each class in the timetable.

### Example Requests

```bash
# Get timetable for the authenticated user
curl -X GET http://myapi.nanocodes.com.ng/timetable/

# Get timetable for the authenticated user on a specific day
curl -X GET http://myapi.nanocodes.com.ng/timetable/get_timetable_by_day/monday

# Create a new timetable entry
curl -X POST -H "Content-Type: application/json" -d '{"course": "Math", "starts": "09:00:00", "ends": "10:30:00", "day": "monday", "category": "alpha"}' http://myapi.nanocodes.com.ng/timetable/create
```

### Example Responses

```json
// Example response for timetable_detail and get_timetable_by_days
[
    {
        "id": 1,
        "course": {
            "id": 1,
            "course_title": "Math",
            "course_description": "Mathematics for beginners",
            "tutor": {
                "id": 1,
                "user": 1,
                "bio": "I am a math tutor",
                "profile_picture": "http://example.com/image.jpg"
            }
        },
        "day": "monday",
        "starts": "09:00:00",
        "ends": "10:30:00"
    },
    // ... more classes
]

// Example response for timetable_create
{
    "course": "Math",
    "starts": "09:00:00",
    "ends": "10:30:00",
    "day": "monday",
    "category": "alpha"
}
```