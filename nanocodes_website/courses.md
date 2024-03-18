## Course API Documentation

This documentation provides an overview of the Course API, which is used to manage and retrieve information about courses.

## Endpoints

### GET https://myapi.nanocodes.com.ng/courses/

- **Description:** Retrieve a list of all available courses.
  
- **Permissions:** AllowAny

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "tutor": {
        "id": 1,
        "tutor_name": "John Doe",
        ...
      },
      "course_title": "Introduction to Python",
      "price": 49.99,
      "description": "A comprehensive course covering Python basics...",
      "what_you_will_learn": "..."
      "what_is_required": "..."
      "course_outline": "..."
      "course_outline_main": "..."
      "no_of_students": 1000,
      "no_of_reviews": 50,
      "background_color": "#FFFFFF",
      "course_icon": "..."
      "slug": "introduction-to-python",
      "image": "..."
      "summary": "..."
      "tags": ["Python", "Programming", ...]
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/{id}/

- **Description:** Retrieve details of a specific course by ID.
  
- **Permissions:** AllowAny

- **Response Body:**
  ```json
  {
    "id": 1,
    "tutor": {
      "id": 1,
      "tutor_name": "John Doe",
      ...
    },
    "course_title": "Introduction to Python",
    "price": 49.99,
    "description": "A comprehensive course covering Python basics...",
    "what_you_will_learn": "..."
    "what_is_required": "..."
    "course_outline": "..."
    "course_outline_main": "..."
    "no_of_students": 1000,
    "no_of_reviews": 50,
    "background_color": "#FFFFFF",
    "course_icon": "..."
    "slug": "introduction-to-python",
    "image": "..."
    "summary": "..."
    "tags": ["Python", "Programming", ...]
  }
  ```

### GET https://myapi.nanocodes.com.ng/courses/courses_that_you_may_like/

- **Description:** Retrieve a list of recommended courses based on user interests.
  
- **Permissions:** AllowAny

- **Response Body:**
  ```json
  [
    {
      "id": 5,
      "tutor": {
        "id": 2,
        "tutor_name": "Jane Smith",
        ...
      },
      "course_title": "Advanced JavaScript",
      "price": 59.99,
      "description": "Master advanced JavaScript concepts...",
      ...
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/user_courses/

- **Description:** Retrieve courses that the authenticated user is enrolled in.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "user": {
        "id": 1,
        "username": "example_user",
        ...
      },
      "course": {
        "id": 1,
        "course_title": "Introduction to Python",
        ...
      },
      "has_paid": true,
      "course_status": "completed",
      ...
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/user_course/{course_id}/

- **Description:** Retrieve details of a specific course that the authenticated user is enrolled in by course ID.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  {
    "id": 1,
    "user": {
      "id": 1,
      "username": "example_user",
      ...
    },
    "course": {
      "id": 1,
      "course_title": "Introduction to Python",
      ...
    },
    "has_paid": true,
    "course_status": "completed",
    ...
  }
  ```

### GET https://myapi.nanocodes.com.ng/courses/get_course_by_slug/{slug}/

- **Description:** Retrieve details of a specific course by slug.
  
- **Permissions:** IsAdminOrReadOnly

- **Response Body:**
  ```json
  {
    "id": 1,
    "tutor": {
      "id": 1,
      "tutor_name": "John Doe",
      ...
    },
    "course_title": "Introduction to Python",
    "price": 49.99,
    "description": "A comprehensive course covering Python basics...",
    "what_you_will_learn": "..."
    "what_is_required": "..."
    "course_outline": "..."
    "course_outline_main": "..."
    "no_of_students": 1000,
    "no_of_reviews": 50,
    "background_color": "#FFFFFF",
    "course_icon": "..."
    "slug": "introduction-to-python",
    "image": "..."
    "summary": "..."
    "tags": ["Python", "Programming", ...]
  }
  ```

### GET https://myapi.nanocodes.com.ng/courses/get_paid_user_courses/

- **Description:** Retrieve courses that the authenticated user has paid for.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "user": {
        "id": 1,
        "username": "example_user",
        ...
      },
      "course": {
        "id": 1,
        "course_title": "Introduction to Python",
        ...
      },
      "has_paid": true,
      "course_status": "completed",
      ...
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/course_pdf_count/

- **Description:** Retrieve the count of courses with PDF outlines.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  {
    "pdf_count": 20
  }
  ```

### GET https://myapi.nanocodes.com.ng/courses/course_count/

- **Description:** Retrieve the total count of courses.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  100
  ```

---


### GET https://myapi.nanocodes.com.ng/courses/get_courses_by_tag/{tag_id}/

- **Description:** Retrieve courses based on a specific tag ID.
  
- **Permissions:** IsAdminOrReadOnly

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "course_title": "Introduction to Python",
      ...
    },
    {
      "id": 2,
      "course_title": "Advanced Python Programming",
      ...
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/get_user_courses_by_tag/{tag_id}/

- **Description:** Retrieve courses based on a specific tag ID that the authenticated user has paid for.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "user": {
        "id": 1,
        "username": "example_user",
        ...
      },
      "course": {
        "id": 1,
        "course_title": "Introduction to Python",
        ...
      },
      "has_paid": true,
      "course_status": "completed",
      ...
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/get_suggested_courses/

- **Description:** Retrieve suggested courses based on the user's interests.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "course_title": "Introduction to Python",
      ...
    },
    {
      "id": 2,
      "course_title": "Advanced Python Programming",
      ...
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/get_featured_courses/

- **Description:** Retrieve featured courses.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "course_title": "Introduction to Python",
      ...
    },
    {
      "id": 2,
      "course_title": "Advanced Python Programming",
      ...
    },
    ...
  ]
  ```

### GET https://myapi.nanocodes.com.ng/courses/get_quick_courses/

- **Description:** Retrieve quick courses.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "course_title": "Introduction to Python",
      ...
    },
    {
      "id": 2,
      "course_title": "Advanced Python Programming",
      ...
    },
    ...
  ]
  ```z

### GET https://myapi.nanocodes.com.ng/courses/get_online_courses/

- **Description:** Retrieve online courses that the authenticated user has paid for.
  
- **Permissions:** IsAuthenticated

- **Response Body:**
  ```json
  [
    {
      "id": 1,
      "course_title": "Introduction to Python",
      ...
    },
    {
      "id": 2,
      "course_title": "Advanced Python Programming",
      ...
    },
    ...
  ]
  ```


**1. Get Paid Courses by Tag (`GET /get_user_courses_by_tag/<int:tag_id>`)**

* **Route:** `/get_user_courses_by_tag/<int:tag_id>`
* **Method:** GET
* **Permissions:** Requires authentication (`IsAuthenticated`)
* **Description:** Retrieves a list of paid courses associated with a specific tag.
* **Request Body:** None
* **Response:**
    * Status Code: 200 OK upon success.
    * Response Body: An array of serialized `UserCourse` objects containing details about the user's enrolled paid courses that are tagged with the provided ID.
    * Error Codes:
        * 401 Unauthorized: If authentication fails.
        * 404 Not Found: If the specified tag is not found.

**2. Upload Course Content (`POST /upload-course-content/`)**

* **Route:** `/upload-course-content/`
* **Method:** POST
* **Permissions:** Requires admin user privileges (`IsAdminUser`)
* **Description:** Uploads course content associated with a course.
* **Request Body:**
    * Required fields:
        * `title`: (string) Title of the course content.
        * `course_description`: (string) Description of the course content (optional).
        * `course`: (integer) ID of the course the content belongs to.
        * `tutor_name` (string): Name of the tutor delivering the content.
        * One of the following (depending on document type):
            * `content_file`: (file) File containing the course content (video).
            * `link`: (URL) Link to the course content (external resource).
            * `document_url`: (file) File containing the course document.
    * Optional fields:
        * `snippet_title`: (string) Title of the content snippet (preview).
        * `snippet_description`: (string) Description of the content snippet (preview).
        * `snippet_file_url`: (file) File containing the content snippet (preview code).
        * `link_title`: (string) Title for the linked content (optional).
        * `document_type`: (string) Type of the uploaded document (PDF, Video, etc.).
        * `document_description`: (string) Description of the uploaded document (optional).
        * `document_title`: (string) Title for the uploaded document (optional).
* **Response:**
    * Status Code: 201 Created upon successful upload.
    * Response Body: A serialized `CourseContent` object representing the newly created course content.
    * Error Codes:
        * 401 Unauthorized: If authentication fails.
        * 400 Bad Request: If required fields are missing or invalid data is provided.



**3. Get Course Content (`GET /<int:course_id>/content/`)**

* **Route:** `/<int:course_id>/content/`
* **Method:** GET
* **Permissions:** Requires authentication (`IsAuthenticated`)
* **Description:** Retrieves all course content associated with a specific course.
* **Request Body:** None
* **Response:**
    * Status Code: 200 OK upon success.
    * Response Body: An array of serialized `CourseContent` objects containing details about the course content for the provided course ID.
    * Error Codes:
        * 401 Unauthorized: If authentication fails.
        * 404 Not Found: If the specified course is not found.

### User Course Content Settings

**Endpoint:** `/user-course-content-settings/`  
**https Methods:** GET, POST, PUT  
**Authentication:** Required  

**Description:**  
Allows users to manage their settings for course content.

#### Request Body (POST):
- `course_content` (integer): ID of the course content
- `review` (string): User review for the course content
- `course_status` (string, optional): Status of the course content (Pending, Completed, ToCompleted)
- `user` (integer): ID of the user
- `rating` (string, optional): Rating for the course content (NoStar, OneStar, TwoStar, ThreeStar, FourStar, FiveStar)

#### Response (GET):
- Status: 200 OK
- Body: List of user course content settings objects

#### Response (POST):
- Status: 201 Created
- Body: Serialized user course content settings object

#### Response (PUT):
- Status: 200 OK
- Body: Serialized updated user course content settings object


## Permissions

- `course_list`: Allows anyone to access.
- `course_detail`: Allows anyone to access.
- `course_pdf_count`: Requires authentication.

## CSRF Exemption

- `course_list`: Exempted from CSRF protection.
- `course_detail`: Exempted from CSRF protection.
- `course_pdf_count`: Exempted from CSRF protection.

## URL Patterns

- `/courses/`: Maps to the `course_list` view.
- `/courses/{id}`: Maps to the `course_detail` view.
- `/courses/course-pdf-count/`: Maps to the `course_pdf_count` view.

## Serializers

- `CourseSerializer`: Serializes the `Course` model.

## Models <a name="models"></a>

### Course Model <a name="course-model"></a>

The `Course` model represents an online course.

- `tutor`: The tutor who created the course.
- `course_title`: Title of the course.
- `price`: Price of the course.
- `description`: Description of the course.
- `what_you_will_learn`: Details of what the user will learn in the course.
- `what_is_required`: Requirements for the course.
- `course_outline`: Image representing the course outline.
- `course_outline_main`: Main file for the course outline.
- `no_of_students`: Number of students enrolled in the course.
- `no_of_reviews`: Number of reviews for the course.
- `background_color`: Background color of the course.
- `course_icon`: Icon representing the course.
- `slug`: Unique slug for the course.
- `image`: Image representing the course.
- `summary`: Summary of the course.
- `tags`: Tags associated with the course.

### UserCourse Model <a name="usercourse-model"></a>

The `UserCourse` model represents the enrollment of a user in a course.

- `user`: The user enrolled in the course.
- `course`: The course in which the user is enrolled.
- `has_paid`: Indicates if the user has paid for the course.
- `course_status`: Status of the user's progress in the course.
- `date_completed`: Date when the course was completed.
- `assignment_recorded`: Number of assignments recorded.
- `progress`: Progress percentage of the user in the course.

### CourseContent Model <a name="coursecontent-model"></a>

The `CourseContent` model represents the content of a course.

- `title`: Title of the content.
- `course_description`: Description of the course content.
- `course`: The course to which the content belongs.
- `tutor_name`: Name of the tutor associated with the content.
- `content_file`: Video File containing the course content.
- `snippet_description`: Description of code snippets.
- `snippet_title`: Title of code snippets.
- `snippet_file_url`: URL of code snippets.
- `link`: URL link related to the content.
- `link_title`: Title of the URL link.
- `document_type`: Type of document associated with the content.
- `document_description`: Description of the document.
- `document_title`: Title of the document.
- `document_url`: URL of the document.

### Announcement Model <a name="announcement-model"></a>

The `Announcement` model represents announcements related to courses.

- `course`: The course associated with the announcement.
- `title`: Title of the announcement.
- `body`: Body text of the announcement.
- `tutor`: The tutor who made the announcement.


## Example Requests

```bash
# List all courses
curl -X GET https://myapi.nanocodes.com.ng/courses/

# Retrieve details of a specific course
curl -X GET https://myapi.nanocodes.com.ng/courses/1

# Count PDF files by course
curl -X GET https://myapi.nanocodes.com.ng/courses/course-pdf-count/
```

## Example Responses

```json
// Example response for course_list
[
    {
        "id": 1,
        "title": "Introduction to Math",
        "description": "A course on basic math concepts",
        "tutor_id": 1,
        // ... other course fields
    },
    // ... more courses
]

// Example response for course_detail
{
    "id": 1,
    "title": "Introduction to Math",
    "description": "A course on basic math concepts",
    "tutor_id": 1,
    // ... other course fields
}

// Example response for course_pdf_count
[
    {
        "course_id": 1,
        "pdf_count": 5
    },
    {
        "course_id": 2,
        "pdf_count": 3
    },
    // ... more courses
]
```

This documentation provides an overview of the Course API endpoints, including the list of courses, course details, and the endpoint for counting PDF files by course. It also includes information about the permissions, CSRF exemption, URL patterns, serializers, and example requests and responses.