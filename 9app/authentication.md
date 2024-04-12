## API Documentation for Retiree Information Management System

### Base URL
All API requests should be made to:
```
https://django-9app-production.up.railway.app/auth/
```

### Endpoints Overview

#### Authentication and User Management

1. **User Registration**
   - `/register/` (POST)

2. **Verify Account**
   - `/verify-account/` (POST)

3. **User Login**
   - `/login/` (POST)

4. **Logout**
   - `/logout/` (POST)

5. **Change Password**
   - `/change-password/` (POST)

6. **Password Reset**
   - `/reset-password/` (POST)

7. **Password Reset Confirmation**
   - `/reset-password/confirm/` (POST)

8. **Resend OTP**
   - `/resend-otp/` (POST)

9. **Verify Login Token (Two-Factor Authentication)**
   - `/verify-login/` (POST)

10. **User Two-Factor Authentication Settings**
    - `/user/2fa/` (PUT)

11. **Verify Token for Password Reset**
    - `/verify-token/` (POST)

12. **List All Users**
    - `/users/` (GET)

### Detailed Endpoint Documentation

#### 1. User Registration
- **Endpoint:** `/register/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Registers a new user. Sends an OTP via email for account activation.
- **Request Body:**
  ```json
  {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "phone_number": "1234567890",
    "password": "securepassword123"
  }
  ```
- **Responses:**
  - **201 Created:** Registration successful; OTP sent.
    ```json
    {
      "status": "success",
      "message": "OTP for account activation sent successfully",
      "entity": null
    }
    ```
  - **400 Bad Request:** Errors like existing email or phone number.
    ```json
    {
      "status": "failure",
      "message": "A user with that email/phone number already exists.",
      "entity": null
    }
    ```

#### 2. Verify Account
- **Endpoint:** `/verify-account/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Verifies the user's email or phone number using an OTP. Activates the user account.
- **Request Body:**
  - **using email:**
  ```json
  {
    "otp": "123456",
    "email": "john.doe@example.com" // shouldn't be there if phone number is provided
  }
  ```
  - **using phone number:**
  ```json
  {
    "otp": "123456",
    "phone_number": "+2348104505457" // shouldn't be there if email is provided
  }
  ```
- **Responses:**
  - **200 OK:** Account verified; user activated.
    ```json
    {
      "status": "success",
      "message": "Account verified successfully",
      "entity": null
    }
    ```
  - **400 Bad Request:** Invalid OTP or missing email/phone number.
    ```json
    {
      "status": "failure",
      "message": "Invalid OTP or required data missing",
      "entity": null
    }
    ```

#### 3. User Login
- **Endpoint:** `/login/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Authenticates user credentials. If two-factor authentication is enabled, sends an OTP.
- **Request Body:**
  ```json
  {
    "email": "john.doe@example.com",
    "password": "securepassword123"
  }
  ```
- **Responses:**
  - **200 OK:** Authentication successful; token or OTP sent based on 2FA status.
    ```json
    {
      "status": "success",
      "message": "Login successful or OTP sent for 2FA",
      "entity": {
        "user": {
          "id": "uuid",
          "email": "john.doe@example.com",
          "first_name": "John",
          "last_name": "Doe",
          "two_factor_enabled": true
        },
        "token": "access_token", // Provided if 2FA is not enabled
        "refresh_token": "refresh_token"
      }
    }
    ```
  - **401 Unauthorized:** Invalid credentials or user inactive.
    ```json
    {
      "status": "failure",
      "message": "Invalid credentials or user not active",
      "entity": null
    }
    ```

#### 4. Logout
- **Endpoint:** `/logout/`
- **Method:** `POST`
- **Permissions:** IsAuthenticated


- **Description:** Logs out a user by blacklisting the refresh token.
- **Request Body:**
  ```json
  {
    "refresh_token": "refresh_token"
  }
  ```
- **Responses:**
  - **200 OK:** Successfully logged out.
    ```json
    {
      "status": "success",
      "message": "User logged out successfully.",
      "entity": null
    }
    ```

#### 5. Change Password
- **Endpoint:** `/change-password/`
- **Method:** `POST`
- **Permissions:** IsAuthenticated
- **Description:** Allows authenticated users to change their password.
- **Request Body:**
  ```json
  {
    "old_password": "currentpassword123",
    "new_password": "newsecurepassword123"
  }
  ```
- **Responses:**
  - **200 OK:** Password changed successfully.
    ```json
    {
      "status": "success",
      "message": "Password changed successfully.",
      "entity": null
    }
    ```
  - **400 Bad Request:** Incorrect old password or validation errors.
    ```json
    {
      "status": "failure",
      "message": "Old password is incorrect or validation failed",
      "entity": null
    }
    ```

#### 6. Password Reset
- **Endpoint:** `/reset-password/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Initiates a password reset process by sending an OTP to the user's email.
- **Request Body:**
  ```json
  {
    "email": "john.doe@example.com"
  }
  ```
- **Responses:**
  - **200 OK:** Password reset OTP sent.
    ```json
    {
      "status": "success",
      "message": "Password reset OTP sent successfully",
      "entity": null
    }
    ```
  - **404 Not Found:** Email not found.
    ```json
    {
      "status": "failure",
      "message": "Email not found",
      "entity": null
    }
    ```

#### 7. Password Reset Confirmation
- **Endpoint:** `/reset-password/confirm/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Confirms the password reset by checking the OTP and setting a new password.
- **Request Body:**
  ```json
  {
    "new_password": "newsecurepassword123",
    "otp": "123456",
    "email": "john.doe@example.com"
  }
  ```
- **Responses:**
  - **200 OK:** Password reset successfully.
    ```json
    {
      "status": "success",
      "message": "Password reset successfully",
      "entity": null
    }
    ```
  - **400 Bad Request:** Invalid OTP or email.
    ```json
    {
      "status": "failure",
      "message": "Invalid OTP or email",
      "entity": null
    }
    ```

#### 8. Resend OTP
- **Endpoint:** `/resend-otp/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Resends the OTP for account verification or password reset.
- **Request Body:**
  ```json
  {
    "email": "john.doe@example.com" // Optional if phone number is provided
  }
  ```
  - **Request Body:**
  ```json
  {
    "phone_number": "+234200349239" // Optional if email is provided
  }
  ```
- **Responses:**
  - **200 OK:** OTP resent successfully.
    ```json
    {
      "status": "success",
      "message": "OTP resent successfully",
      "entity": null
    }
    ```
  - **404 Not Found:** Email or phone number not found.
    ```json
    {
      "status": "failure",
      "message": "Email or phone number not found",
      "entity": null
    }
    ```

#### 9. Verify Login Token (Two-Factor Authentication)
- **Endpoint:** `/verify-login/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Verifies the login attempt by checking the OTP sent during the two-factor authentication process.
- **Request Body:**
  ```json
  {
    "otp": "123456",
    "email": "john.doe@example.com" // Optional if phone number is provided
  }
  ```
- **Responses:**
  - **200 OK:** Verification successful; user authenticated.
    ```json
    {
      "status": "success",
      "message": "Verification successful; user authenticated",
      "entity": {
        "user": {
          "id": "uuid",
          "email": "john.doe@example.com",
          "first_name": "John",
          "last_name": "Doe",
          "two_factor_enabled": true
        },
        "token": "access_token",
        "refresh_token": "refresh_token"
      }


    }
    ```
  - **400 Bad Request:** Invalid OTP or email/phone number.
    ```json
    {
      "status": "failure",
      "message": "Invalid OTP or required data missing",
      "entity": null
    }
    ```

#### 10. User Two-Factor Authentication Settings
- **Endpoint:** `/user/2fa/`
- **Method:** `PUT`
- **Permissions:** IsAuthenticated
- **Description:** Allows authenticated users to enable or disable two-factor authentication.
- **Request Body:**
  ```json
  {
    "two_factor_enabled": true,
    "two_factor_type": "email"
  }
  ```
- **Responses:**
  - **200 OK:** 2FA settings updated successfully.
    ```json
    {
      "status": "success",
      "message": "Two-factor authentication settings updated successfully",
      "entity": null
    }
    ```
  - **400 Bad Request:** Errors in request data.
    ```json
    {
      "status": "failure",
      "message": "Error updating 2FA settings",
      "entity": null
    }
    ```

#### 11. Verify Token for Password Reset
- **Endpoint:** `/verify-token/`
- **Method:** `POST`
- **Permissions:** Allow any
- **Description:** Verifies the OTP sent for password reset and provides a token for submitting the new password.
- **Request Body:**
  ```json
  {
    "email": "john.doe@example.com",
    "otp": "123456"
  }
  ```
- **Responses:**
  - **200 OK:** Token verification successful; new verification code provided.
    ```json
    {
      "status": "success",
      "message": "Token verification successful",
      "new_verification_code": "new_code"
    }
    ```
  - **400 Bad Request:** Invalid OTP or email.
    ```json
    {
      "status": "failure",
      "message": "Invalid OTP or email",
      "entity": null
    }
    ```

#### 12. List All Users
- **Endpoint:** `/users/`
- **Method:** `GET`
- **Permissions:** Admins or specific roles (if applied)
- **Description:** Lists all registered users. Can be restricted to admin users.
- **Responses:**
  - **200 OK:** List of all users.
    ```json
    {
      "status": "success",
      "message": "Users retrieved successfully",
      "entity": [
        {
          "id": "uuid",
          "email": "user1@example.com",
          "first_name": "User",
          "last_name": "One"
        },
        {
          "id": "uuid",
          "email": "user2@example.com",
          "first_name": "User",
          "last_name": "Two"
        }
      ]
    }
    ```
  - **401 Unauthorized:** Unauthorized if the user does not have admin rights.
    ```json
    {
      "status": "failure",
      "message": "Unauthorized access",
      "entity": null
    }
    ```