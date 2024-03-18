# Faq API Documentation

This documentation provides an overview of the Question and Answer API, which is used to manage and retrieve information about questions and their answers.

### Endpoints

#### 1. List Questions

- `GET /question/`: Retrieve a list of all questions.

##### Request

- No parameters are required for this endpoint.

##### Response

- Success: HTTP 200 OK with a list of all questions.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
[
    {
        "id": 1,
        "question": "What is the capital of France?"
    },
    // ... more questions
]
```

#### 2. Retrieve Question Details

- `GET /question/{id}/`: Retrieve details of a specific question.

##### Request

- `id`: The ID of the question.

##### Response

- Success: HTTP 200 OK with the details of the specified question.
- Failure: HTTP 404 Not Found if the question does not exist.

##### Example Response

```json
{
    "id": 1,
    "question": "What is the capital of France?"
}
```

#### 3. List Answers

- `GET /answer/`: Retrieve a list of all answers.

##### Request

- No parameters are required for this endpoint.

##### Response

- Success: HTTP 200 OK with a list of all answers.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
[
    {
        "id": 1,
        "question": {
            "id": 1,
            "question": "What is the capital of France?"
        },
        "answer": "Paris"
    },
    // ... more answers
]
```

#### 4. Retrieve Answer Details

- `GET /answer/{id}/`: Retrieve details of a specific answer.

##### Request

- `id`: The ID of the answer.

##### Response

- Success: HTTP 200 OK with the details of the specified answer.
- Failure: HTTP 404 Not Found if the answer does not exist.

##### Example Response

```json
{
    "id": 1,
    "question": {
        "id": 1,
        "question": "What is the capital of France?"
    },
    "answer": "Paris"
}
```

#### 5. Get Answer by Question

- `GET /get_answer_by_question/{question}`: Retrieve the answer for a specific question.

##### Request

- `question`: The ID of the question.

##### Response

- Success: HTTP 200 OK with the answer for the specified question.
- Failure: HTTP 404 Not Found if the question does not exist or if no answer is found for the question.

##### Example Response

```json
{
    "id": 1,
    "question": {
        "id": 1,
        "question": "What is the capital of France?"
    },
    "answer": "Paris"
}
```

### Permissions

- `QuestionViewSet`: Allows anyone to access.
- `AnswerViewSet`: Allows anyone to access.
- `GetAnswerBySQuestionViewSet`: Allows anyone to access.

### URL Patterns

- `/question/`: Maps to the `QuestionViewSet` view.
- `/answer/`: Maps to the `AnswerViewSet` view.
- `/get_answer_by_question/{question}`: Maps to the `GetAnswerBySQuestionViewSet` view.

### Serializers

- `QuestionSerializer`: Serializes the `Question` model.
- `AnswerSerializer`: Serializes the `Answer` model.

### Models

- `Question`: Represents a question with a text field for the question.
- `Answer`: Represents an answer with a foreign key to the `Question` model and a text field for the answer.

### Example Requests

```bash
# List all questions
curl -X GET http://myapi.nanocodes.com.ng/faq/question/

# Retrieve details of a specific question
curl -X GET http://myapi.nanocodes.com.ng/faq/question/1/

# List all answers
curl -X GET http://myapi.nanocodes.com.ng/faq/answer/

# Retrieve details of a specific answer
curl -X GET http://myapi.nanocodes.com.ng/faq/answer/1/

# Get answer by question
curl -X GET http://myapi.nanocodes.com.ng/faq/get_answer_by_question/1
```

### Example Responses

```json
// Example response for QuestionViewSet
[
    {
        "id": 1,
        "question": "What is the capital of France?"
    },
    // ... more questions
]

// Example response for AnswerViewSet
[
    {
        "id": 1,
        "question": {
            "id": 1,
            "question": "What is the capital of France?"
        },
        "answer": "Paris"
    },
    // ... more answers
]

// Example response for GetAnswerBySQuestionViewSet
{
    "id": 1,
    "question": {
        "id": 1,
        "question": "What is the capital of France?"
    },
    "answer": "Paris"
}
```

