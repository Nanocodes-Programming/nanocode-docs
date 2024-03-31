Sure, here's a comprehensive documentation tailored to the frontend covering all APIs and URLs:

---

## User Authentication and Management APIs Documentation

### Register a New User
- **URL:** `/register/`
- **Method:** `POST`
- **Description:** Registers a new user with the system.
- **Request Body:**
  - `fullname` (string, required): Full name of the user.
  - `username` (string, required): Username chosen by the user.
  - `email` (string, required): Email address of the user.
  - `password` (string, required): Password for the user account.
- **Response:**
  - `message` (string): Success message.
  - `token` (string): Access token for authentication.
  - `refresh_token` (string): Refresh token for obtaining new access tokens.

### Verify Account Activation
- **URL:** `/verify-account/`
- **Method:** `POST`
- **Description:** Verifies the account activation using OTP.
- **Request Body:**
  - `otp` (string, required): OTP sent to the user's email for verification.
  - `email` (string, required): Email address of the user.
- **Response:**
  - `message` (string): Success message upon successful account verification.

### User Login
- **URL:** `/login/`
- **Method:** `POST`
- **Description:** Logs in a user to the system.
- **Request Body:**
  - `email` (string, required): Email address of the user.
  - `password` (string, required): Password for the user account.
- **Response:**
  - `user` (object): User details.
  - `token` (string): Access token for authentication.
  - `refresh_token` (string): Refresh token for obtaining new access tokens.
  - `message` (string): Success message.

### Verify Two-Factor Authentication Login
- **URL:** `/verify-login/`
- **Method:** `POST`
- **Description:** Verifies the two-factor authentication login using OTP.
- **Request Body:**
  - `email` (string, required): Email address of the user.
  - `otp` (string, required): OTP sent to the user's email for verification.
- **Response:**
  - `user` (object): User details.
  - `token` (string): Access token for authentication.
  - `refresh_token` (string): Refresh token for obtaining new access tokens.
  - `message` (string): Success message.

### Enable/Disable Two-Factor Authentication
- **URL:** `/user/2fa/`
- **Method:** `PUT`
- **Description:** Enables or disables two-factor authentication for the user.
- **Request Body:**
  - `two_factor_enabled` (boolean, required): Enable/disable two-factor authentication.
- **Response:**
  - `message` (string): Success message.

### Token Refresh
- **URL:** `/token/refresh/`
- **Method:** `POST`
- **Description:** Refreshes the access token using the refresh token.
- **Response:**
  - `access` (string): New access token.

### List All Users
- **URL:** `/users/`
- **Method:** `GET`
- **Description:** Retrieves a list of all users in the system.
- **Response:**
  - List of user objects containing user details.

### Logout
- **URL:** `/logout/`
- **Method:** `POST`
- **Description:** Logs out the user from the system.
- **Request Body:**
  - `refresh_token` (string, required): Refresh token.
- **Response:**
  - `message` (string): Success message.

### Change Password
- **URL:** `/change-password/`
- **Method:** `POST`
- **Description:** Allows the user to change their password.
- **Request Body:**
  - `old_password` (string, required): Current password.
  - `new_password` (string, required): New password.
- **Response:**
  - `message` (string): Success message.
  - `refresh_token` (string): Refresh token for obtaining new access tokens.

### Initiate Password Reset
- **URL:** `/reset-password/`
- **Method:** `POST`
- **Description:** Initiates the password reset process and sends an OTP to the user's email.
- **Request Body:**
  - `email` (string, required): Email address of the user.
- **Response:**
  - `message` (string): Success message.

### Confirm Password Reset
- **URL:** `/reset-password/confirm/`
- **Method:** `POST`
- **Description:** Confirms the password reset by verifying the OTP and setting a new password.
- **Request Body:**
  - `email` (string, required): Email address of the user.
  - `otp` (string, required): OTP sent to the user's email for verification.
  - `new_password` (string, required): New password to set.
- **Response:**
  - `message` (string): Success message.

---

These APIs provide functionalities for user registration, authentication, password management, and account activation. Make sure to handle responses and errors appropriately in the frontend application.