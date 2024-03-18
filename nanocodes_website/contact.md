# Contact App API Documentation

## Introduction

Welcome to the API documentation for Contact. This API allows users to submit their contact information and messages for communication purposes.

## Authentication

No authentication is required to access the endpoints of this API. All endpoints are open to public access.

## Base URL

```
https://myapi.nanocodes.com.ng/contact/
```

## Endpoints

### 1. Create Contact

#### Description

This endpoint allows users to submit their contact information and messages. Upon successful submission, an email notification is sent to the provided email address, and a copy is forwarded to the admin.

#### HTTP Method

```
POST
```

#### Parameters

- `name`: Name of the contact (string, required)
- `email`: Email of the contact (string, required)
- `message`: Message from the contact (string, required)

#### Request URL

```
/contact/create/
```

#### Request Body

```json
{
    "name": "John Doe",
    "email": "john@example.com",
    "message": "This is a test message."
}
```

#### Response Example

```json
{
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "message": "This is a test message."
}
```

#### Response Codes

- 201: Contact created successfully
- 400: Bad request (Invalid data provided)

#### Sample Error Response

```json
{
    "error": "Invalid email address"
}
```

### 2. Retrieve Contact

#### Description

This endpoint retrieves the details of a specific contact by its ID.

#### HTTP Method

```
GET
```

#### Parameters

- `id`: ID of the contact (integer, required)

#### Request URL

```
/contact/<id>/
```

#### Response Example

```json
{
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "message": "This is a test message."
}
```

#### Response Codes

- 200: Contact details retrieved successfully
- 404: Contact not found

## Error Handling

- 400: Bad Request - This error occurs if the request body is missing or contains invalid data.
- 404: Not Found - This error occurs if the requested contact ID does not exist.
- 500: Internal Server Error - This error occurs if there's a server-side issue.

## Rate Limiting

This API does not impose any rate limiting restrictions.
