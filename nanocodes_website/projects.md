# Projects API Documentation

This documentation provides an overview of the Projects API, which is used to manage and retrieve information about projects.

### Endpoints

#### 1. Project ViewSet

The `ProjectViewSet` provides the following endpoints:

- `GET /`: Retrieve a list of all projects.
- `POST /`: Create a new project.
- `GET /<id>/`: Retrieve a specific project by its ID.
- `PUT /<id>/`: Update a specific project by its ID.
- `PATCH /<id>/`: Partially update a specific project by its ID.
- `DELETE /<id>/`: Delete a specific project by its ID.
- `POST /get_total/`: Get the total number of projects.

##### Request

- For the `GET`, `PUT`, `PATCH`, and `DELETE` methods, the ID of the project is required in the URL.
- For the `POST` method, the request body should contain the details of the project.
- For the `get_total` action, no request body is required.

##### Response

- Success: HTTP 200 OK for `GET`, `POST`, `PUT`, `PATCH`, and `DELETE` methods. For the `get_total` action, the response is the total number of projects.
- Failure: HTTP 400 Bad Request if the request is not valid, or HTTP 404 Not Found if the project does not exist.

##### Example Response

```json
// Example response for GET /<id>/
{
    "id": 1,
    "image": "http://example.com/path/to/image.jpg",
    "project_name": "Project Name"
}

// Example response for get_total
3
```

### Permissions

- `ProjectViewSet`: Allows anyone to access the `GET` and `get_total` actions. Authentication is required for the `POST`, `PUT`, `PATCH`, and `DELETE` methods.

### URL Patterns

- `/`: Maps to the `ProjectViewSet` with the default actions (`list`, `create`, `retrieve`, `update`, `partial_update`, `destroy`).
- `/<id>/`: Maps to the `ProjectViewSet` with the default actions (`list`, `create`, `retrieve`, `update`, `partial_update`, `destroy`) for a specific project.
- `/get_total/`: Maps to the `get_total` action of the `ProjectViewSet`.

### Serializer

- `ProjectsSerializer`: Serializes the `Projects` model.

### Model

- `Projects`: Represents a project with fields for image and project_name.

### Example Requests

```bash
# Retrieve a list of all projects
curl -X GET http://myapi.nanocodes.com.ng/project/

# Create a new project
curl -X POST http://myapi.nanocodes.com.ng/project/ -d '{"image": "http://example.com/path/to/image.jpg", "project_name": "Project Name"}'

# Retrieve a specific project
curl -X GET http://myapi.nanocodes.com.ng/project/<id>/

# Update a specific project
curl -X PUT http://myapi.nanocodes.com.ng/project/<id>/ -d '{"image": "http://example.com/path/to/new-image.jpg", "project_name": "New Project Name"}'

# Partially update a specific project
curl -X PATCH http://myapi.nanocodes.com.ng/project/<id>/ -d '{"project_name": "Updated Project Name"}'

# Delete a specific project
curl -X DELETE http://myapi.nanocodes.com.ng/project/<id>/

# Get the total number of projects
curl -X POST http://myapi.nanocodes.com.ng/project/get_total/
```

### Example Responses

```json
// Example response for GET /<id>/
{
    "id": 1,
    "image": "http://example.com/path/to/image.jpg",
    "project_name": "Project Name"
}

// Example response for get_total
3
```

### Notes

- The `ProjectViewSet` uses the `ProjectsSerializer` for serialization and deserialization of the `Projects` model.
- The `get_total` action is a custom action that returns the total number of projects.
- The `@action` decorator is used to define custom actions on the viewset.
- The `permission_classes` attribute is used to specify the permissions for each action.
- The `AllowAny` permission class allows unauthenticated users to access the `get_total` action, while authenticated users are required for the other actions.

Remember to replace `<id>` in the URL with the actual ID of the project you want to retrieve, update, or delete. Also, replace `<token>` in the `Authorization: Bearer <token>` header with a valid JWT token for the actions that require authentication.
