## User Authentication and Management API Documentation

This documentation provides an overview of the User API, which is used to manage user registration, login, verification, password reset, and user details.

## Endpoints

### 1. User Registration

- `POST /auth/register/`: Register a new user.

#### Request

- Body: A JSON object containing the user's email, password, and other required fields.

#### Response

- Success: HTTP 201 Created with the user details and JWT tokens.
- Failure: HTTP 400 Bad Request with error message.

### 2. User Verification

- `POST /auth/verify_user/`: Verify a user's email.

#### Request

- Body: A JSON object containing the OTP code.

#### Response

- Success: HTTP 200 OK with a success message.
- Failure: HTTP 400 Bad Request with error message.

### 3. User Login

- `POST /auth/login/`: Log in a user.

#### Request

- Body: A JSON object containing the user's email and password.

#### Response

- Success: HTTP 200 OK with the user details and JWT tokens.
- Failure: HTTP 401 Unauthorized with error message.

### 4. Password Reset

- `POST /auth/password_reset/`: Initiate a password reset for a user.

#### Request

- Body: A JSON object containing the user's email.

#### Response

- Success: HTTP 200 OK with a success message.
- Failure: HTTP 400 Bad Request with error message.
- Failure: HTTP 500 Internal Server Error with error message.

### 5. Confirm Password Reset

- `POST /auth/confirm_password/`: Confirm a password reset for a user.

#### Request

- Body: A JSON object containing the verification code and the new password.

#### Response

- Success: HTTP 200 OK with the user details and new JWT tokens.
- Failure: HTTP 400 Bad Request with error message.

### 6. User Details

- `GET /user/`: Retrieve the details of the authenticated user.
- `PUT /user/`: Update the details of the authenticated user.
- `DELETE /user/`: Delete the authenticated user.

#### Request

- Authentication: Requires a valid JWT token.

#### Response

- Success: HTTP 200 OK with the user details.
- Failure: HTTP 401 Unauthorized if the user is not authenticated.
- Failure: HTTP 404 Not Found if the user does not exist.

## Permissions

- `UserRegistrationView`: Allows anyone to register.
- `VerifyUserView`: Allows anyone to verify.
- `UserLoginView`: Allows anyone to log in.
- `PasswordResetView`: Allows anyone to request a password reset.
- `PasswordConfirmationView`: Allows anyone to confirm a password reset.
- `UserDetailUpdateDeleteView`: Requires authentication.

## URL Patterns

- `/auth/register/`: Maps to the `UserRegistrationView` view for user registration.
- `/auth/verify_user/`: Maps to the `VerifyUserView` view for user verification.
- `/auth/login/`: Maps to the `UserLoginView` view for user login.
- `/auth/password_reset/`: Maps to the `PasswordResetView` view for password reset.
- `/auth/confirm_password/`: Maps to the `PasswordConfirmationView` view for password confirmation.
- `/user/`: Maps to the `UserDetailUpdateDeleteView` view for user details.

## Serializers

- `CustomRegisterSerializer`: Serializes the `User` model for registration.
- `VerifyUserOtpSerializer`: Serializes the `User` model for OTP verification.
- `EmailSerializer`: Serializes the `User` model for email.
- `PasswordResetConfirmationSerializer`: Serializes the `User` model for password reset confirmation.
- `CustomTokenObtainPairSerializer`: Serializes the `User` model for token generation.
- `UserSerializer`: Serializes the `User` model for user details.

## Models

- `User`: Represents a user with fields for email, password, OTP, and other user-related information.

## Example Requests

```bash
# User Registration
curl -X POST -H "Content-Type: application/json" -d '{"email": "user@example.com", "password": "password123"}' http://myapi.nanocodes.com.ng/auth/register/

# User Verification
curl -X POST -H "Content-Type: application/json" -d '{"otp": "123456"}' http://myapi.nanocodes.com.ng/auth/verify_user/

# User Login
curl -X POST -H "Content-Type: application/json" -d '{"email": "user@example.com", "password": "password123"}' http://myapi.nanocodes.com.ng/auth/login/

# Password Reset
curl -X POST -H "Content-Type: application/json" -d '{"email": "user@example.com"}' http://myapi.nanocodes.com.ng/auth/password_reset/

# Confirm Password Reset
curl -X POST -H "Content-Type: application/json" -d '{"verification_code": "123456", "password": "newpassword123"}' http://myapi.nanocodes.com.ng/auth/confirm_password/

# Retrieve User Details
curl -X GET -H "Authorization: Bearer <token>" http://myapi.nanocodes.com.ng/user/
```

## Example Responses

```json
// Example response for UserRegistrationView
{
    "refresh": "<refresh_token>",
    "access": "<access_token>",
    "user": {
        "email": "user@example.com",
        // ... other user fields
    }
}

// Example response for VerifyUserView
{
    "User": "User verified successfully"
}

// Example response for UserLoginView
{
    "refresh": "<refresh_token>",
    "access": "<access_token>",
    "user": {
        "email": "user@example.com",
        // ... other user fields
    }
}

// Example response for PasswordResetView
{
    "message": "password reset verification code sent"
}

// Example response for PasswordConfirmationView
{
    "access": "<new_access_token>",
    "refresh": "<new_refresh_token>",
    "user": {
        "email": "user@example.com",
        // ... other user fields
    }
}

// Example response for UserDetailUpdateDeleteView
{
    "email": "user@example.com",
    // ... other user fields
}
```

This documentation provides an overview of the User API endpoints, including user registration, login, verification, password reset, and user details. It includes information about the permissions, URL patterns, serializers, and example requests and responses.