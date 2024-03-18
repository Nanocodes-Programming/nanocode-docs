# ChatGPT API Documentation

## Introduction

Welcome to the API documentation for ChatGPT. This API allows users to ask questions and receive AI-generated answers using OpenAI's GPT models.

## Authentication

Authentication is required to access the endpoints of this API. Users must be authenticated to interact with the chatbot.

## Base URL

```
https://myapi.nanocodes.com.ng/chatgpt/
```

## Endpoints

### 1. Ask Question and Get Answer

#### Description

This endpoint allows users to ask questions and receive AI-generated answers using OpenAI's GPT models.

#### HTTP Method

```
POST
```

#### Parameters

- `text`: Text of the question (string, required)

#### Request URL

```
/chatgpt/questions/
```

#### Request Body

```json
{
    "text": "What is the capital of France?"
}
```

#### Response Example

```json
{
    "answer": "The capital of France is Paris.",
    "question": {
        "id": 1,
        "text": "What is the capital of France?"
    }
}
```

#### Response Codes

- 201: Question and answer created successfully
- 400: Bad request (Invalid data provided)

#### Sample Error Response

```json
{
    "error": "Invalid question format"
}
```

### 2. Get Answers by Question ID

#### Description

This endpoint retrieves all answers corresponding to a specific question ID.

#### HTTP Method

```
GET
```

#### Parameters

- `id`: ID of the question (integer, required)

#### Request URL

```
/chatgpt/get_answers_by_id/<id>/
```

#### Response Example

```json
[
    {
        "id": 1,
        "question": 1,
        "answer": "The capital of France is Paris."
    }
]
```

#### Response Codes

- 200: Answers retrieved successfully
- 404: Question not found

## Error Handling

- 400: Bad Request - This error occurs if the request body is missing or contains invalid data.
- 404: Not Found - This error occurs if the requested question ID does not exist.
- 500: Internal Server Error - This error occurs if there's a server-side issue.

## Rate Limiting

This API does not impose any rate limiting restrictions.

