# Service API Documentation

This documentation provides an overview of the API endpoints and their functionality.

### Endpoints

#### 1. Service Views

- `GET /services/`: Retrieve a list of all services.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "name": "Service 1",
            "description": "Description of Service 1",
            // ... other fields
        },
        // ... other services
    ]
    ```

- `GET /services/<int:pk>/`: Retrieve details of a specific service by its ID.

    **Request**: None

    **Response**:
    ```json
    {
        "id": 1,
        "name": "Service 1",
        "description": "Description of Service 1",
        // ... other fields
    }
    ```

#### 2. Portfolio Views

- `GET /portfolio/`: Retrieve a list of all portfolio items.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "title": "Portfolio 1",
            "description": "Description of Portfolio 1",
            "category": {
                "id": 1,
                "name": "Category 1",
                // ... other category fields
            },
            // ... other portfolio fields
        },
        // ... other portfolio items
    ]
    ```

- `GET /portfolio/<int:category_id>/`: Retrieve a list of portfolio items filtered by category ID.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "title": "Portfolio 1",
            "description": "Description of Portfolio 1",
            "category": {
                "id": 1,
                "name": "Category 1",
                // ... other category fields
            },
            // ... other portfolio fields
        },
        // ... other portfolio items in the specified category
    ]
    ```

#### 3. Company Views

- `GET /company/`: Retrieve a list of all companies.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "name": "Company 1",
            "description": "Description of Company 1",
            // ... other company fields
        },
        // ... other companies
    ]
    ```

#### 4. Tag Views

- `GET /tag/`: Retrieve a list of all tags.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "name": "Tag 1",
            // ... other tag fields
        },
        // ... other tags
    ]
    ```

- `POST /tag/`, `GET /tag/<int:pk>/`, `PUT /tag/<int:pk>/`, `PATCH /tag/<int:pk>/`, `DELETE /tag/<int:pk>/`: Similar to the `FeatureView` and `VideoView` endpoints, these require authentication and handle CRUD operations for tags.

#### 5. Feature Views

- `GET /features/`: Retrieve a list of all features.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "name": "Feature 1",
            // ... other feature fields
        },
        // ... other features
    ]
    ```

- `POST /features/`, `GET /features/<int:pk>/`, `PUT /features/<int:pk>/`, `PATCH /features/<int:pk>/`, `DELETE /features/<int:pk>/`: Similar to the `TagView` and `VideoView` endpoints, these require authentication and handle CRUD operations for features.

#### 6. Video Views

- `GET /video/`: Retrieve a list of all videos.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "title": "Video 1",
            "url": "http://example.com/video1",
            // ... other video fields
        },
        // ... other videos
    ]
    ```

- `POST /video/`, `GET /video/<int:pk>/`, `PUT /video/<int:pk>/`, `PATCH /video/<int:pk>/`, `DELETE /video/<int:pk>/`: Similar to the `TagView` and `FeatureView` endpoints, these require authentication and handle CRUD operations for videos.

#### 7. Count Views

- `GET /get_code_snippet_count/`: Retrieve the count of code snippets.

    **Request**: None

    **Response**:
    ```json
    {
        "count": 10
    }
    ```

- `GET /get_links_count/`: Retrieve the count of links.

    **Request**: None

    **Response**:
    ```json
    {
        "count": 20
    }
    ```

- `GET /get_videos_count/`: Retrieve the count of videos.

    **Request**: None

    **Response**:
    ```json
    {
        "count": 30
    }
    ```

### Permissions

- `ServiceList`, `ServiceDetail`, `PortfolioView`, `CompanyView`, `PortfolioByCategoryView`: Allow anyone to access these views.
- `TagView`, `FeatureView`, `VideoView`: Require authentication for all actions except `GET` and `HEAD`.
- `get_code_snippet_count`, `link_count`, `video_count`: Require authentication.

### Serializers

- `ServiceSerializer`: Serializes the `Service` model.
- `CategorySerializer`: Serializes the `Category` model.
- `PortfolioSerializer`: Serializes the `Portfolio` model, including the `Category` model through a nested serializer.
- `CompanySerializer`: Serializes the `Company` model.
- `VideoSerializer`: Serializes the `Video` model.
- `FeatureSerializer`: Serializes the `Features` model.
- `TagSerializer`: Serializes the `Tag` model.
- `CodeSnippetCountSerializer`: Serializes the count of code snippets.

### Example Requests


```bash
# Delete a specific tag
curl -X DELETE http://myapi.nanocodes.com.ng/tag/<int:pk>/ -H "Authorization: Bearer <token>"

# Retrieve a list of all features
curl -X GET http://myapi.nanocodes.com.ng/features/

# Create a new feature
curl -X POST http://myapi.nanocodes.com.ng/features/ -d '{"name": "New Feature"}' -H "Content-Type: application/json" -H "Authorization: Bearer <token>"

# Retrieve details of a specific feature
curl -X GET http://myapi.nanocodes.com.ng/features/<int:pk>/

# Update a specific feature
curl -X PUT http://myapi.nanocodes.com.ng/features/<int:pk>/ -d '{"name": "Updated Feature"}' -H "Content-Type: application/json" -H "Authorization: Bearer <token>"

# Partially update a specific feature
curl -X PATCH http://myapi.nanocodes.com.ng/features/<int:pk>/ -d '{"name": "Partially Updated Feature"}' -H "Content-Type: application/json" -H "Authorization: Bearer <token>"

# Delete a specific feature
curl -X DELETE http://myapi.nanocodes.com.ng/features/<int:pk>/ -H "Authorization: Bearer <token>"

# Retrieve a list of all videos
curl -X GET http://myapi.nanocodes.com.ng/video/

# Create a new video
curl -X POST http://myapi.nanocodes.com.ng/video/ -d '{"title": "New Video", "url": "http://example.com/video"}' -H "Content-Type: application/json" -H "Authorization: Bearer <token>"

# Retrieve details of a specific video
curl -X GET http://myapi.nanocodes.com.ng/video/<int:pk>/

# Update a specific video
curl -X PUT http://myapi.nanocodes.com.ng/video/<int:pk>/ -d '{"title": "Updated Video"}' -H "Content-Type: application/json" -H "Authorization: Bearer <token>"

# Partially update a specific video
curl -X PATCH http://myapi.nanocodes.com.ng/video/<int:pk>/ -d '{"title": "Partially Updated Video"}' -H "Content-Type: application/json" -H "Authorization: Bearer <token>"

# Delete a specific video
curl -X DELETE http://myapi.nanocodes.com.ng/video/<int:pk>/ -H "Authorization: Bearer <token>"

# Retrieve the count of code snippets
curl -X GET http://myapi.nanocodes.com.ng/get_code_snippet_count/ -H "Authorization: Bearer <token>"

# Retrieve the count of links
curl -X GET http://myapi.nanocodes.com.ng/get_links_count/ -H "Authorization: Bearer <token>"

# Retrieve the count of videos
curl -X GET http://myapi.nanocodes.com.ng/get_videos_count/ -H "Authorization: Bearer <token>"
```

Replace `<int:pk>` with the actual ID of the service, tag, feature, or video you want to retrieve, update, or delete. Replace `<int:category_id>` with the actual ID of the category to filter portfolio items. Replace `<token>` with a valid JWT token for the actions that require authentication.

Remember to include the `Authorization: Bearer <token>` header with a valid JWT token for the actions that require authentication.
