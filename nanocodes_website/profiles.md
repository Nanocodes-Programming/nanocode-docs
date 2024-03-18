# Profile API Documentation

This documentation provides an overview of the Profile API, which is used to manage and retrieve information about user profiles.

### Endpoints

#### 1. Retrieve User Profile

- `GET /`: Retrieve the profile of the authenticated user.

##### Request

- Authentication is required.

##### Response

- Success: HTTP 200 OK with the details of the user's profile.
- Failure: HTTP 401 Unauthorized if the user is not authenticated.

##### Example Response

```json
{
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "image": "http://example.com/path/to/image.jpg",
    "instagramUrl": "https://www.instagram.com/johndoe",
    "twitterUrl": "https://www.twitter.com/johndoe",
    "linkedinUrl": "https://www.linkedin.com/in/johndoe"
}
```

#### 2. Create or Update User Profile

- `POST /create`: Create or update the profile of the authenticated user.

##### Request

- Authentication is required.
- Body:
  - `first_name`: The first name of the user.
  - `last_name`: The last name of the user.
  - `email`: The email address of the user.
  - `image`: The profile image of the user.
  - `instagramUrl`: The Instagram URL of the user.
  - `twitterUrl`: The Twitter URL of the user.
  - `linkedinUrl`: The LinkedIn URL of the user.

##### Response

- Success: HTTP 200 OK with the updated details of the user's profile.
- Failure: HTTP 400 Bad Request with error message if the data is not valid.

##### Example Response

```json
{
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "image": "http://example.com/path/to/image.jpg",
    "instagramUrl": "https://www.instagram.com/johndoe",
    "twitterUrl": "https://www.twitter.com/johndoe",
    "linkedinUrl": "https://www.linkedin.com/in/johndoe"
}
```

### Permissions

- `profile_detail`: Requires authentication.
- `profile_create`: Requires authentication.

### URL Patterns

- `/`: Maps to the `profile_detail` view.
- `/create`: Maps to the `profile_create` view.

### Serializers

- `ProfileSerializer`: Serializes the user profile for retrieval.
- `ProfileCreateSerializer`: Serializes the user profile for creation or update.

### Example Requests

```bash
# Retrieve user profile
curl -X GET http://myapi.nanocodes.com.ng/profile/ -H "Authorization: Bearer <token>"

# Create or update user profile
curl -X POST http://myapi.nanocodes.com.ng/profile/create -H "Authorization: Bearer <token>" -d '{"first_name": "John", "last_name": "Doe", "email": "john.doe@example.com", "image": "http://example.com/path/to/image.jpg", "instagramUrl": "https://www.instagram.com/johndoe", "twitterUrl": "https://www.twitter.com/johndoe", "linkedinUrl": "https://www.linkedin.com/in/johndoe"}'
```

### Example Responses

```json
// Example response for profile_detail
{
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "image": "http://example.com/path/to/image.jpg",
    "instagramUrl": "https://www.instagram.com/johndoe",
    "twitterUrl": "https://www.twitter.com/johndoe",
    "linkedinUrl": "https://www.linkedin.com/in/johndoe"
}

// Example response for profile_create
{
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "image": "http://example.com/path/to/image.jpg",
    "instagramUrl": "https://www.instagram.com/johndoe",
    "twitterUrl": "https://www.twitter.com/johndoe",
    "linkedinUrl": "https://www.linkedin.com/in/johndoe"
}
```

### Notes

- The `profile_detail` view retrieves the profile of the authenticated user.
- The `profile_create` view creates or updates the profile of the authenticated user.
- The `raise_exception=True` parameter in `serializer.is_valid()` will automatically return a 400 response with the validation errors if the data is not valid.
- The `@csrf_exempt` decorator is used to allow POST requests from other domains, which is generally not recommended due to security reasons. If you need to allow cross-domain requests, consider using Django's CORS settings or a third-party package like `django-cors-headers`.
- The `clean_image` method in the `ProfileCreateSerializer` is commented out because it seems to be intended for image renaming, which is not a standard operation in Django. Django's `ImageField` automatically handles file uploads and storage. If you need to perform additional operations on the image, such as resizing or cropping, you would typically use a library like Pillow in a custom `save()` method on the model.

Remember to replace `<token>` in the `Authorization: Bearer <token>` header with a valid JWT token for the `profile_detail` and `profile_create` endpoints.
