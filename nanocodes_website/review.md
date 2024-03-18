# Reviews API Documentation

This documentation provides an overview of the Client Reviews API, which is used to manage and retrieve information about client reviews.

### Endpoints

#### 1. Client Reviews ViewSet

The `ClientReviewsViewSet` provides the following endpoints:

- `GET /`: Retrieve a list of all client reviews.
- `POST /`: Create a new client review.
- `GET /<id>/`: Retrieve a specific client review by its ID.
- `PUT /<id>/`: Update a specific client review by its ID.
- `PATCH /<id>/`: Partially update a specific client review by its ID.
- `DELETE /<id>/`: Delete a specific client review by its ID.

##### Request

- For the `GET`, `PUT`, `PATCH`, and `DELETE` methods, the ID of the client review is required in the URL.
- For the `POST` method, the request body should contain the details of the client review.

##### Response

- Success: HTTP 200 OK for `GET`, `POST`, `PUT`, `PATCH`, and `DELETE` methods.
- Failure: HTTP 400 Bad Request if the request is not valid, or HTTP 404 Not Found if the client review does not exist.

##### Example Response

```json
// Example response for GET /<id>/
{
    "id": 1,
    "project": 1,
    "user": 1,
    "review": "This is a great project!",
    "client_rating": "fivestar"
}
```

### Permissions

- `ClientReviewsViewSet`: Allows anyone to access all actions.

### URL Patterns

- `/`: Maps to the `ClientReviewsViewSet` with the default actions (`list`, `create`, `retrieve`, `update`, `partial_update`, `destroy`).
- `/<id>/`: Maps to the `ClientReviewsViewSet` with the default actions (`list`, `create`, `retrieve`, `update`, `partial_update`, `destroy`) for a specific client review.

### Serializer

- `ClientReviewsSerializer`: Serializes the `ClientReviews` model.

### Model

- `ClientReviews`: Represents a client review with fields for project, user, review, and client_rating.

### Example Requests

```bash
# Retrieve a list of all client reviews
curl -X GET http://myapi.nanocodes.com.ng/reviews/

# Create a new client review
curl -X POST http://myapi.nanocodes.com.ng/reviews/ -d '{"project": 1, "user": 1, "review": "This is a great project!", "client_rating": "fivestar"}'

# Retrieve a specific client review
curl -X GET http://myapi.nanocodes.com.ng/reviews/<id>/

# Update a specific client review
curl -X PUT http://myapi.nanocodes.com.ng/reviews/<id>/ -d '{"review": "This is an excellent project!"}'

# Partially update a specific client review
curl -X PATCH http://myapi.nanocodes.com.ng/reviews/<id>/ -d '{"client_rating": "fivestar"}'

# Delete a specific client review
curl -X DELETE http://myapi.nanocodes.com.ng/reviews/<id>/
```

### Example Responses

```json
// Example response for GET /<id>/
{
    "id": 1,
    "project": 1,
    "user": 1,
    "review": "This is a great project!",
    "client_rating": "fivestar"
}
```

### Notes

- The `ClientReviewsViewSet` uses the `ClientReviewsSerializer` for serialization and deserialization of the `ClientReviews` model.
- The `permission_classes` attribute is used to specify the permissions for each action.
- The `AllowAny` permission class allows unauthenticated users to access all actions.

Remember to replace `<id>` in the URL with the actual ID of the client review you want to retrieve, update, or delete.
