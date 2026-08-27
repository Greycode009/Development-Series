# Day 24 — E-Commerce API: Authentication & Authorization

## 📌 Overview

Today I continued building the **E-Commerce API** with Node.js, Express, MongoDB, and Mongoose.

The main focus was implementing a complete **authentication and authorization system**, including **OTP-based email verification, Argon2id password hashing, JWT authentication, session management, HTTP-only cookies, logout, and role-based authorization**.

---

## Project Repository

🔗 [E-commerce API — GitHub](https://github.com/Greycode009/E-commerce-API.git)

## 🚀 What I Built

### 👤 User System

Created the User model with:

- Name
- Email
- Password
- Role
- Verification status
- Timestamps

Supported roles:

- `consumer`
- `merchant`
- `admin`

---

## 🔐 User Registration

Implemented user registration with:

- Email uniqueness check
- Password validation
- Argon2id password hashing
- User creation
- Account verification status

Passwords are never stored as plain text.

```text
User Password
      ↓
   Argon2id
      ↓
Hashed Password
      ↓
    MongoDB
```

---

## 📧 OTP Email Verification

Implemented OTP-based account verification.

### Added

- 6-digit OTP generation
- OTP hashing using SHA-256
- 10-minute OTP expiration
- MongoDB TTL index
- OTP email delivery
- OTP verification
- Used OTP deletion
- Resend OTP functionality

OTP flow:

```text
Register
   ↓
Generate OTP
   ↓
Hash OTP
   ↓
Store OTP
   ↓
Send OTP Email
   ↓
User enters OTP
   ↓
Verify OTP
   ↓
Account Verified
```

---

## 🔑 Login & JWT Authentication

Implemented login using email and password.

### Added

- Verified-user check
- Argon2id password verification
- Access token generation
- Refresh token generation
- JWT expiration configuration

Authentication flow:

```text
Email + Password
       ↓
Verify Credentials
       ↓
Generate JWT
       ↓
Access Token
       ↓
Authenticated Requests
```

---

## 🔄 Session Management

Implemented server-side session management for refresh tokens.

Created:

- Session model
- User-session relationship
- Refresh token storage
- Session expiration

```text
Login
  ↓
Refresh Token
  ↓
Session Created
  ↓
MongoDB
```

---

## 🍪 HTTP-Only Refresh Token Cookie

Refresh tokens are stored in an **HTTP-only cookie** instead of being returned directly in the response body.

### Authentication structure

```text
Access Token
     ↓
Returned in JSON response
     ↓
Used for authenticated API requests


Refresh Token
     ↓
HTTP-only Cookie
     ↓
Used to refresh access token
```

This keeps the refresh token inaccessible to client-side JavaScript.

---

## ♻️ Access Token Refresh

Implemented refresh-token authentication.

```text
Refresh Token Cookie
        ↓
Find Session
        ↓
Verify Refresh Token
        ↓
Find User
        ↓
Generate New Access Token
```

Endpoint:

```text
POST /api/users/refresh-token
```

---

## 🚪 Logout

Implemented logout functionality.

### Logout Current Device

```text
Refresh Token
      ↓
Find Session
      ↓
Delete Session
      ↓
Clear Cookie
```

Endpoint:

```text
POST /api/users/logout
```

### Logout All Devices

Implemented logout from all active sessions.

```text
Authenticated User
       ↓
Find All Sessions
       ↓
Delete User Sessions
       ↓
Clear Refresh Token Cookie
```

Endpoint:

```text
POST /api/users/logout-all
```

---

## 🛡️ Authentication Middleware

Implemented authentication middleware using the access token.

The middleware:

- Reads the `Authorization` header
- Extracts the Bearer token
- Verifies the JWT
- Attaches authenticated user information to `req.user`

```text
Authorization: Bearer <accessToken>
              ↓
        JWT Verification
              ↓
           req.user
              ↓
            next()
```

---

## 🔒 Role-Based Authorization

Implemented reusable role-based authorization middleware.

Supported roles:

```text
consumer
merchant
admin
```

Example:

```js
authorize("admin")
```

Multiple roles can also be allowed:

```js
authorize("merchant", "admin")
```

Authorization flow:

```text
Request
   ↓
Authentication
   ↓
req.user
   ↓
Check User Role
   ↓
Access Allowed / Denied
```

Unauthorized users receive:

```text
403 Access Denied
```

---

## 🧪 Testing

Tested the complete authentication flow:

- User registration
- OTP email delivery
- OTP verification
- Invalid OTP
- OTP expiration
- Resend OTP
- Already verified user
- Login
- Invalid credentials
- JWT generation
- Refresh token
- Session creation
- HTTP-only cookie
- Logout
- Logout from all devices
- Authentication middleware
- `req.user`
- Role-based authorization

All implemented authentication and authorization flows were tested successfully.

---

## 🧠 Concepts Reinforced

- Authentication vs Authorization
- Password hashing with Argon2id
- OTP generation and verification
- SHA-256 hashing for short-lived OTP storage
- MongoDB TTL indexes
- JWT access and refresh tokens
- HTTP-only cookies
- Session management
- Authentication middleware
- `req.user`
- Role-based access control
- Controller vs Service responsibilities
- Protected routes
- Refresh-token flow
- Logout and session revocation

---

## 📌 Current Status

### Authentication

**Complete ✅**

### Authorization

**Complete ✅**

### OTP Verification

**Complete ✅**

### JWT & Sessions

**Complete ✅**

### Testing

**Complete ✅**

### Git Workflow

**Complete ✅**

Implemented the feature using:

```text
Issue
  ↓
Feature Branch
  ↓
Implement
  ↓
Test
  ↓
Commit
  ↓
Pull Request
  ↓
Review
  ↓
Merge
  ↓
Delete Branch
```

---

## 🔜 Next — Day 25

Continue building the E-Commerce API by connecting the authenticated user system with the existing application features.

The Cart system can now move away from the temporary `consumerId` approach and use the authenticated user from:

```js
req.user
```

---

**Day 24 complete. Authentication secured. Authorization added. 🔐🔥**
