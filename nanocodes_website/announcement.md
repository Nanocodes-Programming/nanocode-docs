# Announcement App API Documentation

## Introduction

Welcome to the API documentation for Announcement. This API allows users to retrieve announcements.

## Authentication

No authentication is required to access the endpoints of this API. All endpoints are open to public access.

## Base URL

```
https://myapi.nanocodes.com.ng/announcements/
```

## Endpoints

### 1. List Announcements

#### Description

This endpoint lists all announcements available in the system.

#### HTTP Method

```
GET
```

#### Parameters

None

#### Request URL

```
/announcements/
```

#### Response Example

```json
[
    {
        "id": 1,
        "title": "Important Announcement",
        "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
    },
    {
        "id": 2,
        "title": "Upcoming Event",
        "content": "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
    }
]
```

#### Response Codes

- 200: Announcements retrieved successfully

## Error Handling

- 500: Internal Server Error - This error occurs if there's a server-side issue.

## Rate Limiting

This API does not impose any rate limiting restrictions.

