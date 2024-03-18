# Newsletter API Documentation

This documentation provides an overview of the Newsletter API, which is used to manage and retrieve information about newsletter subscriptions.

### Endpoints

#### 1. Create a Newsletter Subscription

- `POST /`: Subscribe to the newsletter.

##### Request

- Body:
  - `email`: The email address of the subscriber.
  - `send_me_an_email`: A boolean indicating whether the subscriber wants to receive emails.

##### Response

- Success: HTTP 201 Created with the details of the created subscription.
- Failure: HTTP 400 Bad Request with error message.

##### Example Response

```json
{
    "id": 1,
    "email": "user@example.com",
    "send_me_an_email": true
}
```

### Permissions

- `newsletter_create`: Allows anyone to access.

### URL Patterns

- `/`: Maps to the `newsletter_create` view.

### Serializer

- `NewsletterSerializer`: Serializes the `Newsletter` model.

### Model

- `Newsletter`: Represents a newsletter subscription with fields for email and send_me_an_email.

### Example Requests

```bash
# Subscribe to the newsletter
curl -X POST http://myapi.nanocodes.com.ng/newsletter/ -d '{"email": "user@example.com", "send_me_an_email": true}'
```

### Example Responses

```json
// Example response for newsletter_create
{
    "id": 1,
    "email": "user@example.com",
    "send_me_an_email": true
}
```

### Notes

- The `send_subscribe_mail` function is called after a successful subscription to send a welcome email to the subscriber.
- The `newsletter_create` view is decorated with `@csrf_exempt` to allow POST requests from other domains, which is generally not recommended due to security reasons. If you need to allow cross-domain requests, consider using Django's CORS settings or a third-party package like `django-cors-headers`.
- The `raise_exception=True` parameter in `serializer.is_valid()` will automatically return a 400 response with the validation errors if the data is not valid.

