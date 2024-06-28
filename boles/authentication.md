# Authentication

## Table of Contents
1. [User Login](#user-login)
2. [Create User](#create-user)
3. [Change Password](#change-password)
4. [Reset Password](#reset-password)
5. [Confirm Password Reset](#confirm-password-reset)
6. [Verify Token](#verify-token)
7. [Logout](#logout)

---

## 1. User Login

**Endpoint:** `/login/`  
**Method:** `POST`  
**Permissions:** Allow any  

**Description:** Authenticates user credentials and returns an access token and a refresh token for subsequent requests.

### Request Body:
```json
{
  "email": "john.doe@example.com",
  "password": "securepassword123"
}
```

### Responses:
**200 OK:** Authentication successful; token or OTP sent based on 2FA status.
```json
{
  "status": "success",
  "message": "Login successful",
  "entity": {
    "user": {
      "id": "uuid",
      "email": "john.doe@example.com",
      "first_name": "John",
      "last_name": "Doe"
    },
    "token": "access_token",
    "refresh_token": "refresh_token"
  }
}
```

**401 Unauthorized:** Invalid credentials or user inactive.
```json
{
  "status": "failure",
  "message": "Invalid login details or Email and password are required",
  "entity": null
}
```

---

## 2. Create User

**Endpoint:** `/create-user/`  
**Method:** `POST`  
**Permissions:** IsAdminUser  

**Description:** Creates a new user account. An email with account details and a password reset request is sent to the user.

### Request Body:
```json
{
  "email": "new.user@example.com",
  "first_name": "New",
  "last_name": "User",
  "phone_number": "1234567890",
  "warehouse": 1,
  "role": 2
}
```

### Responses:
**201 Created:** User created successfully.
```json
{
  "status": "success",
  "message": "User created successfully",
  "entity": {
    "id": "uuid",
    "email": "new.user@example.com",
    "first_name": "New",
    "last_name": "User",
    "phone_number": "1234567890",
    "warehouse": 1,
    "role": 2,
    "is_active": true,
    "is_staff": false,
    "is_admin": false
  }
}
```

**400 Bad Request:** Validation errors.
```json
{
  "status": "failure",
  "message": "Validation errors",
  "entity": null
}
```

---

## 3. Change Password

**Endpoint:** `/change-password/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated  

**Description:** Allows authenticated users to change their password.

### Request Body:
```json
{
  "current_password": "oldpassword123",
  "new_password": "newsecurepassword123"
}
```

### Responses:
**200 OK:** Password changed successfully.
```json
{
  "status": "success",
  "message": "Password set"
}
```

**400 Bad Request:** Incorrect current password or validation errors.
```json
{
  "status": "failure",
  "message": "Current password is incorrect or validation errors",
  "entity": null
}
```

---

## 4. Reset Password

**Endpoint:** `/reset-password/`  
**Method:** `POST`  
**Permissions:** IsAdminUser  

**Description:** Allows admins to reset a user's password. A new password is emailed to the user.

### Request Body:
```json
{
  "email": "user.to.reset@example.com"
}
```

### Responses:
**200 OK:** Password reset email sent.
```json
{
  "status": "success",
  "message": "Password reset successful"
}
```

**400 Bad Request:** Email not found or validation errors.
```json
{
  "status": "failure",
  "message": "User with this email does not exist or validation errors",
  "entity": null
}
```

---

## 5. Confirm Password Reset

**Endpoint:** `/password-reset-confirmation/`  
**Method:** `POST`  
**Permissions:** Allow any  

**Description:** Confirms a password reset request using OTP.

### Request Body:
```json
{
  "email": "user.to.reset@example.com",
  "otp": "123456",
  "new_password": "newsecurepassword123"
}
```

### Responses:
**200 OK:** Password reset successfully.
```json
{
  "status": "success",
  "message": "Password reset successfully"
}
```

**400 Bad Request:** Invalid OTP or validation errors.
```json
{
  "status": "failure",
  "message": "Invalid OTP or validation errors",
  "entity": null
}
```

---

## 6. Verify Token

**Endpoint:** `/verify-token/`  
**Method:** `POST`  
**Permissions:** Allow any  

**Description:** Verifies an OTP and generates a new verification code.

### Request Body:
```json
{
  "email": "user@example.com",
  "otp": "123456"
}
```

### Responses:
**200 OK:** Token verified and new verification code generated.
```json
{
  "status": "success",
  "message": "OTP verified",
  "entity": {
    "new_verification_code": "new_code"
  }
}
```

**400 Bad Request:** Invalid OTP or validation errors.
```json
{
  "status": "failure",
  "message": "Invalid OTP or validation errors",
  "entity": null
}
```

---

## 7. Logout

**Endpoint:** `/logout/`  
**Method:** `POST`  
**Permissions:** IsAuthenticated  

**Description:** Logs out the user by invalidating the refresh token.

### Request Body:
```json
{
  "refresh_token": "refresh_token"
}
```

### Responses:
**200 OK:** User logged out successfully.
```json
{
  "status": "success",
  "message": "User logged out successfully"
}
```

**400 Bad Request:** Validation errors.
```json
{
  "status": "failure",
  "message": "Validation errors",
  "entity": null
}
```
