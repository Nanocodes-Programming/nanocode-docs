# Payment API Documentation

This documentation provides an overview of the Payment API, which is used to manage and retrieve information about payments and transactions.

## Endpoints

### 1. List Payment Transactions

- `GET /payment/`: Retrieve a list of all payment transactions for the authenticated user.

#### Request

- Authentication: Requires a valid session token.

#### Response

- Success: HTTP 200 OK with a list of all payment transactions for the authenticated user.
- Failure: HTTP 401 Unauthorized if the user is not authenticated.

#### Example Response

```json
[
    {
        "id": 1,
        "user": 1,
        "course": 1,
        "amount": 1000.00,
        "payment_channel": "paystack",
        "reference_id": "ref123",
        "payment_status": "success",
        // ... other payment fields
    },
    // ... more transactions
]
```

### 2. Initiate Payment

- `POST /payment/`: Initiate a payment for a course.

#### Request

- Authentication: Requires a valid session token.
- Body: A JSON object containing the course ID and the payment channel.

#### Request Body Example

```json
{
    "course": 1,
    "payment_channel": "paystack"
}
```

#### Response

- Success: HTTP 200 OK with the payment details and the response from the payment gateway.
- Failure: HTTP 400 Bad Request if the payment fails or the course does not exist.
- Failure: HTTP 401 Unauthorized if the user is not authenticated.
- Failure: HTTP 400 Bad Request if the user has already paid for the course.

#### Example Response

```json
{
    "data": {
        "payment_response": {
            // Payment gateway response
        },
        "payment": {
            "id": 1,
            "user": 1,
            "course": 1,
            "amount": 1000.00,
            "payment_channel": "paystack",
            "reference_id": "ref123",
            "payment_status": "success",
            // ... other payment fields
        }
    },
    "message": "Payment initiated successfully"
}
```

### 3. Verify Payment

- `GET /payment/verify/{reference}`: Verify a payment transaction.

#### Request

- Authentication: Requires a valid session token.
- Path Parameter: `reference` - The reference ID of the payment transaction.

#### Response

- Success: HTTP 200 OK with the payment details and the verification status.
- Failure: HTTP 404 Not Found if the payment transaction does not exist.
- Failure: HTTP 401 Unauthorized if the user is not authenticated.
- Failure: HTTP 400 Bad Request if the payment verification fails.

#### Example Response

```json
{
    "payment": {
        "id": 1,
        "user": 1,
        "course": 1,
        "amount": 1000.00,
        "payment_channel": "paystack",
        "reference_id": "ref123",
        "payment_status": "success",
        // ... other payment fields
    },
    "message": "Your transaction: success"
}
```

## Permissions

- `PaymentTransactionViewSet`: Requires authentication.
- `PaymentViewSet`: Requires authentication.
- `VerifyPayment`: Requires authentication.

## URL Patterns

- `/payment/`: Maps to the `PaymentTransactionViewSet` view for listing payment transactions.
- `/payment/`: Maps to the `PaymentViewSet` view for initiating a payment.
- `/payment/verify/{reference}`: Maps to the `VerifyPayment` view for verifying a payment.

## Serializers

- `PaymentSerializer`: Serializes the `Payment` model.

## Models

- `Payment`: Represents a payment transaction with fields for user, course, amount, payment channel, reference ID, and payment status.

## Example Requests

```bash
# List all payment transactions
curl -X GET -H "Authorization: Token <token>" http://myapi.nanocodes.com.ng/payment/

# Initiate a payment
curl -X POST -H "Authorization: Token <token>" -H "Content-Type: application/json" -d '{"course": 1, "payment_channel": "paystack"}' http://myapi.nanocodes.com.ng/payment/

# Verify a payment
curl -X GET -H "Authorization: Token <token>" http://myapi.nanocodes.com.ng/payment/verify/ref123
```

## Example Responses

```json
// Example response for PaymentTransactionViewSet
[
    {
        "id": 1,
        "user": 1,
        "course": 1,
        "amount": 1000.00,
        "payment_channel": "paystack",
        "reference_id": "ref123",
        "payment_status": "success",
        // ... other payment fields
    },
    // ... more transactions
]

// Example response for PaymentViewSet
{
    "data": {
        "payment_response": {
            // Payment gateway response
        },
        "payment": {
            "id": 1,
            "user": 1,
            "course": 1,
            "amount": 1000.00,
            "payment_channel": "paystack",
            "reference_id": "ref123",
            "payment_status": "success",
            // ... other payment fields
        }
    },
    "message": "Payment initiated successfully"
}

// Example response for VerifyPayment
{
    "payment": {
        "id": 1,
        "user": 1,
        "course": 1,
        "amount": 1000.00,
        "payment_channel": "paystack",
        "reference_id": "ref123",
        "payment_status": "success",
        // ... other payment fields
    },
    "message": "Your transaction: success"
}
```

This documentation provides an overview of the Payment API endpoints, including the list of payment transactions, payment initialization, and payment verification. It includes information about the permissions, URL patterns, serializers, and example requests and responses.