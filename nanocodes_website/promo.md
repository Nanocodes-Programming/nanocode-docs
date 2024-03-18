# Promo API Documentation

This documentation provides an overview of the Promo API, which is used to manage and retrieve information about promotions.

### Endpoints

#### 1. Promo ViewSet

The `PromoViewSet` provides the following endpoints:

- `GET /`: Retrieve a list of all promotions.
- `POST /`: Create a new promotion.
- `GET /<id>/`: Retrieve a specific promotion by its ID.
- `PUT /<id>/`: Update a specific promotion by its ID.
- `PATCH /<id>/`: Partially update a specific promotion by its ID.
- `DELETE /<id>/`: Delete a specific promotion by its ID.

##### Request

- For the `GET`, `PUT`, `PATCH`, and `DELETE` methods, the ID of the promotion is required in the URL.
- For the `POST` method, the request body should contain the details of the promotion.

##### Response

- Success: HTTP 200 OK for `GET`, `POST`, `PUT`, `PATCH`, and `DELETE` methods.
- Failure: HTTP 400 Bad Request if the request is not valid, or HTTP 404 Not Found if the promotion does not exist.

##### Example Response

```json
// Example response for GET /<id>/
{
    "id": 1,
    "image": "http://example.com/path/to/image.jpg",
    "description": "Promotion Description",
    "link": "http://example.com/promotion",
    "start_date": "2022-01-01",
    "end_date": "2022-12-31",
    "title": "Promotion Title"
}
```

### Permissions

- `PromoViewSet`: Allows anyone to access all actions.

### URL Patterns

- `/`: Maps to the `PromoViewSet` with the default actions (`list`, `create`, `retrieve`, `update`, `partial_update`, `destroy`).
- `/<id>/`: Maps to the `PromoViewSet` with the default actions (`list`, `create`, `retrieve`, `update`, `partial_update`, `destroy`) for a specific promotion.

### Serializer

- `PromoSerializer`: Serializes the `Promo` model.

### Model

- `Promo`: Represents a promotion with fields for image, description, link, start_date, end_date, and title.

### Example Requests

```bash
# Retrieve a list of all promotions
curl -X GET http://myapi.nanocodes.com.ng/promo/

# Create a new promotion
curl -X POST http://myapi.nanocodes.com.ng/promo/ -d '{"image": "http://example.com/path/to/image.jpg", "description": "Promotion Description", "link": "http://example.com/promotion", "start_date": "2022-01-01", "end_date": "2022-12-31", "title": "Promotion Title"}'

# Retrieve a specific promotion
curl -X GET http://myapi.nanocodes.com.ng/promo/<id>/

# Update a specific promotion
curl -X PUT http://myapi.nanocodes.com.ng/promo/<id>/ -d '{"title": "Updated Promotion Title"}'

# Partially update a specific promotion
curl -X PATCH http://myapi.nanocodes.com.ng/promo/<id>/ -d '{"description": "Updated Promotion Description"}'

# Delete a specific promotion
curl -X DELETE http://myapi.nanocodes.com.ng/promo/<id>/
```

### Example Responses

```json
// Example response for GET /<id>/
{
    "id": 1,
    "image": "http://example.com/path/to/image.jpg",
    "description": "Promotion Description",
    "link": "http://example.com/promotion",
    "start_date": "2022-01-01",
    "end_date": "2022-12-31",
    "title": "Promotion Title"
}
```

### Notes

- The `PromoViewSet` uses the `PromoSerializer` for serialization and deserialization of the `Promo` model.
- The `permission_classes` attribute is used to specify the permissions for each action.
- The `AllowAny` permission class allows unauthenticated users to access all actions.

Remember to replace `<id>` in the URL with the actual ID of the promotion you want to retrieve, update, or delete.
