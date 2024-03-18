# API Documentation for Testimonial

This documentation provides an overview of the Testimonial API, which is used to manage and retrieve information about testimonials.

### Endpoints

The `TestimonialViewSet` provides the following endpoints:

#### 1. List and Create Testimonials

- `GET /`: Retrieve a list of all testimonials.

    **Request**: None

    **Response**:
    ```json
    [
        {
            "id": 1,
            "name": "Testimonial 1",
            "stack": "Stack 1",
            "testimonial": "This is a testimonial.",
            "image": "http://example.com/image1.jpg",
            "rating": "onestar"
        },
        // ... other testimonials
    ]
    ```

- `POST /`: Create a new testimonial.

    **Request**:
    ```json
    {
        "name": "New Testimonial",
        "stack": "New Stack",
        "testimonial": "This is a new testimonial.",
        "image": "http://example.com/new-image.jpg",
        "rating": "fivestar"
    }
    ```

    **Response**:
    ```json
    {
        "id": 2,
        "name": "New Testimonial",
        "stack": "New Stack",
        "testimonial": "This is a new testimonial.",
        "image": "http://example.com/new-image.jpg",
        "rating": "fivestar"
    }
    ```

#### 2. Retrieve, Update, Partial Update, and Delete Testimonials

- `GET /<int:pk>/`: Retrieve details of a specific testimonial by its ID.

    **Request**: None

    **Response**:
    ```json
    {
        "id": 1,
        "name": "Testimonial 1",
        "stack": "Stack 1",
        "testimonial": "This is a testimonial.",
        "image": "http://example.com/image1.jpg",
        "rating": "onestar"
    }
    ```

- `PUT /<int:pk>/`: Update a specific testimonial by its ID.

    **Request**:
    ```json
    {
        "name": "Updated Testimonial",
        "stack": "Updated Stack",
        "testimonial": "This is an updated testimonial.",
        "image": "http://example.com/updated-image.jpg",
        "rating": "fivestar"
    }
    ```

    **Response**:
    ```json
    {
        "id": 1,
        "name": "Updated Testimonial",
        "stack": "Updated Stack",
        "testimonial": "This is an updated testimonial.",
        "image": "http://example.com/updated-image.jpg",
        "rating": "fivestar"
    }
    ```

- `PATCH /<int:pk>/`: Partially update a specific testimonial by its ID.

    **Request**:
    ```json
    {
        "testimonial": "Partially updated testimonial."
    }
    ```

    **Response**:
    ```json
    {
        "id": 1,
        "name": "Updated Testimonial",
        "stack": "Updated Stack",
        "testimonial": "Partially updated testimonial.",
        "image": "http://example.com/updated-image.jpg",
        "rating": "fivestar"
    }
    ```

- `DELETE /<int:pk>/`: Delete a specific testimonial by its ID.

    **Request**: None

    **Response**:
    ```json
    {
        "detail": "Testimonial deleted successfully."
    }
    ```

### Permissions

- `TestimonialViewSet`: Allows anyone to access these endpoints.

### Serializers

- `TestimonialSerializer`: Serializes the `Testimonial` model.

### Example Requests

```bash
# Retrieve a list of all testimonials
curl -X GET http://myapi.nanocodes.com.ng/testimonial/

# Create a new testimonial
curl -X POST http://myapi.nanocodes.com.ng/testimonial/ -d '{"name": "New Testimonial", "stack": "New Stack", "testimonial": "This is a new testimonial.", "image": "http://example.com/new-image.jpg", "rating": "fivestar"}' -H "Content-Type: application/json"

# Retrieve details of a specific testimonial
curl -X GET http://myapi.nanocodes.com.ng/testimonial/<int:pk>/

# Update a specific testimonial
curl -X PUT http://myapi.nanocodes.com.ng/testimonial/<int:pk>/ -d '{"name": "Updated Testimonial", "stack": "Updated Stack", "testimonial": "This is an updated testimonial.", "image": "http://example.com/updated-image.jpg", "rating": "fivestar"}' -H "Content-Type: application/json"

# Partially update a specific testimonial
curl -X PATCH http://myapi.nanocodes.com.ng/testimonial/<int:pk>/ -d '{"testimonial": "Partially updated testimonial."}' -H "Content-Type: application/json"

# Delete a specific testimonial
curl -X DELETE http://myapi.nanocodes.com.ng/testimonial/<int:pk>/
```

### Notes

- Replace `<int:pk>` with the actual ID of the testimonial you want to retrieve, update, or delete.
- The `TestimonialViewSet` allows anyone to access these endpoints.
- The `TestimonialSerializer` serializes the `Testimonial` model, including all fields.
- When creating or updating a testimonial, you need to provide the `name`, `stack`, `testimonial`, `image`, and `rating` fields.
- The `image` field should be a URL or path to the image file.
- The `rating` field should be one of the choices from the `Rating` model choices.

Remember to include the `Content-Type: application/json` header when sending JSON data in the request body.
