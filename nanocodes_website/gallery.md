# Gallery API Documentation

This documentation provides an overview of the Gallery API, which is used to manage and retrieve information about galleries.

### Endpoints

#### 1. List Galleries

- `GET /`: Retrieve a list of all approved galleries.

##### Request

- No parameters are required for this endpoint.

##### Response

- Success: HTTP 200 OK with a list of all approved galleries.
- Failure: HTTP 400 Bad Request with error message.

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
        "title": "Gallery Title",
        "about": "About the gallery",
        "image": "path/to/image.jpg",
        "views": 10,
        "approved": true,
        "gallery_category": "upcoming",
        // ... other gallery fields
    },
    // ... more galleries
]
```

#### 2. Retrieve Gallery Details

- `GET /{id}`: Retrieve details of a specific gallery.

##### Request

- `id`: The ID of the gallery.

##### Response

- Success: HTTP 200 OK with the details of the specified gallery.
- Failure: HTTP 404 Not Found if the gallery does not exist or is not approved.

##### Example Response

```json
{
    "id": 1,
    "user": {
        "id": 1,
        "username": "user1",
        "email": "user1@example.com",
        // ... other user fields
    },
    "title": "Gallery Title",
    "about": "About the gallery",
    "image": "path/to/image.jpg",
    "views": 10,
    "approved": true,
    "gallery_category": "upcoming",
    // ... other gallery fields
}
```

#### 3. Create a Gallery

- `POST /create/`: Create a new gallery.

##### Request

- Authentication is required.
- Body:
  - `title`: The title of the gallery.
  - `about`: The description of the gallery.
  - `image`: The image associated with the gallery.

##### Response

- Success: HTTP 201 Created with the details of the created gallery.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
{
    "id": 1,
    "title": "Gallery Title",
    "about": "About the gallery",
    "image": "path/to/image.jpg",
    "views": 0,
    "approved": false,
    "gallery_category": "upcoming",
    // ... other gallery fields
}
```

#### 4. Get Galleries by Category

- `GET /get_gallery_by_category/{gallery_category}`: Retrieve a list of galleries by category.

##### Request

- `gallery_category`: The category of the galleries.

##### Response

- Success: HTTP 200 OK with a list of galleries in the specified category.
- Failure: HTTP 404 Not Found if no galleries are found in the category.

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
        "title": "Gallery Title",
        "about": "About the gallery",
        "image": "path/to/image.jpg",
        "views": 10,
        "approved": true,
        "gallery_category": "upcoming",
        // ... other gallery fields
    },
    // ... more galleries
]
```

#### 5. Get Trending Galleries

- `GET /get_trending_gallery/`: Retrieve a list of the top 10 trending galleries.

##### Request

- No parameters are required for this endpoint.

##### Response

- Success: HTTP 200 OK with a list of the top 10 trending galleries.
- Failure: HTTP 400 Bad Request with error message.

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
        "title": "Gallery Title",
        "about": "About the gallery",
        "image": "path/to/image.jpg",
        "views": 100,
        "approved": true,
        "gallery_category": "upcoming",
        // ... other gallery fields
    },
    // ... more galleries
]
```

### Permissions

- `gallery_list`: Allows anyone to access.
- `gallery_detail`: Allows anyone to access.
- `GalleryCreateView`: Requires authentication.
- `GetGalleryByCategoryViewSet`: Requires authentication.
- `GetTrendingGalleryViewSet`: Requires authentication.

### URL Patterns

- `/`: Maps to the `gallery_list` view.
- `/{id}`: Maps to the `gallery_detail` view.
- `/create/`: Maps to the `GalleryCreateView` view.
- `/get_gallery_by_category/{gallery_category}`: Maps to the `GetGalleryByCategoryViewSet` view.
- `/get_trending_gallery/`: Maps to the `GetTrendingGalleryViewSet` view.

### Serializers

- `UserGallerySerializer`: Serializes the `User` model.
- `GallerySerializer`: Serializes the `Gallery` model.
- `GalleryCreateSerializer`: Serializes the `Gallery` model for creation.

### Models

- `GalleryCategory`: An enumeration of the possible gallery categories.
- `ApprovedGalleryManager`: A manager that filters out unapproved galleries.
- `Gallery`: Represents a gallery with fields for user, title, about, image, views, approved, and gallery_category.

### Example Requests

```bash
# List all approved galleries
curl -X GET http://myapi.nanocodes.com.ng/gallery/

# Retrieve details of a specific gallery
curl -X GET http://myapi.nanocodes.com.ng/gallery/1

# Create a new gallery
curl -X POST http://myapi.nanocodes.com.ng/gallery/create/ -H "Authorization: Bearer <token>" -d '{"title": "New Gallery", "about": "About the new gallery", "image": "path/to/image.jpg"}'

# Get galleries by category
curl -X GET http://myapi.nanocodes.com.ng/gallery/get_gallery_by_category/upcoming

# Get trending galleries
curl -X GET http://myapi.nanocodes.com.ng/gallery/get_trending_gallery/
```

### Example Responses

```json
// Example response for gallery_list
[
    {
        "id": 1,
        "user": {
            "id": 1,
            "username": "user1",
            "email": "user1@example.com",
            // ... other user fields
        },
        "title": "Gallery Title",
        "about": "About the gallery",
        "image": "path/to/image.jpg",
        "views": 10,
        "approved": true,
        "gallery_category": "upcoming",
        // ... other gallery fields
    },
    // ... more galleries
]

// Example response for gallery_detail
```json
{
    "id": 1,
    "user": {
        "id": 1,
        "username": "user1",
        "email": "user1@example.com",
        // ... other user fields
    },
    "title": "Gallery Title",
    "about": "About the gallery",
    "image": "path/to/image.jpg",
    "views": 10,
    "approved": true,
    "gallery_category": "upcoming",
    // ... other gallery fields
}

// Example response for GalleryCreateView
{
    "id": 1,
    "title": "New Gallery",
    "about": "About the new gallery",
    "image": "path/to/image.jpg",
    "views": 0,
    "approved": false,
    "gallery_category": "upcoming",
    // ... other gallery fields
}

// Example response for GetGalleryByCategoryViewSet
[
    {
        "id": 1,
        "user": {
            "id": 1,
            "username": "user1",
            "email": "user1@example.com",
            // ... other user fields
        },
        "title": "Gallery Title",
        "about": "About the gallery",
        "image": "path/to/image.jpg",
        "views": 10,
        "approved": true,
        "gallery_category": "upcoming",
        // ... other gallery fields
    },
    // ... more galleries
]

// Example response for GetTrendingGalleryViewSet
[
    {
        "id": 1,
        "user": {
            "id": 1,
            "username": "user1",
            "email": "user1@example.com",
            // ... other user fields
        },
        "title": "Gallery Title",
        "about": "About the gallery",
        "image": "path/to/image.jpg",
        "views": 100,
        "approved": true,
        "gallery_category": "upcoming",
        // ... other gallery fields
    },
    // ... more galleries
]
```

Note: The `ApprovedGalleryManager` is used to filter out unapproved galleries. The `gallery_category` field is an instance of `GalleryCategory`, which is a `TextChoices` enumeration. The `views` field is incremented each time the gallery is viewed, and the `approved` field indicates whether the gallery has been approved for display.

The `clean_image` method in the `GalleryCreateSerializer` is commented out because it seems to be intended for image renaming, which is not a standard operation in Django. Django's `ImageField` automatically handles file uploads and storage. If you need to perform additional operations on the image, such as resizing or cropping, you would typically use a library like Pillow in a custom `save()` method on the model.

Remember to replace `<token>` in the `Authorization: Bearer <token>` header with a valid JWT token for the `GalleryCreateView` endpoint.