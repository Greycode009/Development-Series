# Day 25 — E-Commerce API: Merchant Registration

## 📌 Overview

Today I continued building the **E-Commerce API** with Node.js, Express, MongoDB, and Mongoose.

The main focus was building the **foundation of the Merchant system**, including merchant registration, business information, validation, and merchant approval status.

---

## Project Repository

🔗 [E-commerce API — GitHub](https://github.com/Greycode009/E-commerce-API.git)

## 🚀 What I Built

### 🏪 Merchant Feature

Created a dedicated Merchant feature following the existing project structure:

```text
features/
└── merchant/
    ├── merchant.model.js
    ├── merchant.controllers.js
    ├── merchant.routes.js
    └── merchant.service.js
```

### 📝 Merchant Registration

Implemented a separate merchant registration flow.

Endpoint:

```text
POST /api/merchant
```

Merchant registration includes:

- Name
- Email
- Password
- Business name
- Business description

The registration creates:

```text
User
  ↓
role: merchant

Merchant
  ↓
status: pending
```

### 🏪 Merchant Model

Created the Merchant model with:

- User ID
- Business name
- Business description
- Application status
- Reviewed by
- Reviewed at
- Timestamps

Application statuses:

```text
pending
approved
rejected
```

New merchant registrations automatically start with:

```text
status: pending
```

### ✅ Merchant Validation

Added Zod validation for merchant registration.

Validated:

- Name
- Email
- Password
- Business name
- Business description

### 🔐 Security

Applied the existing Argon2id password hashing system to merchant registration.

Also ensured that the hashed password is **not returned in the API response**.

Example response:

```json
{
  "user": {
    "name": "Test Merchant",
    "email": "merchant@example.com",
    "role": "merchant",
    "verified": false
  },
  "merchant": {
    "businessName": "Tech Store",
    "status": "pending"
  }
}
```

### 🧠 Concepts Reinforced

- Feature-based project structure
- Separate merchant domain
- Mongoose relationships using ObjectId
- Zod validation
- Argon2id password hashing
- Role-based user accounts
- Merchant approval workflow
- Controller vs Service responsibilities
- API response security

### 🧪 Testing

Tested merchant registration successfully.

Verified that:

- Merchant account is created
- User receives `merchant` role
- Merchant status starts as `pending`
- Business information is stored
- Password is not exposed in the response

### 📌 Current Status

**Merchant Registration — Complete ✅**

**Merchant Approval — Pending 🚧**

**OTP Verification — Pending 🚧**

**Merchant Authorization — Pending 🚧**

The merchant onboarding feature is being implemented across multiple steps.

---

## 🔜 Next — Day 26

Continue the Merchant Onboarding system:

- Connect merchant registration with OTP verification
- Implement admin merchant review
- Implement merchant approval
- Implement merchant rejection
- Restrict pending merchants from merchant functionality
- Test the complete merchant onboarding flow

---

**Day 25 complete. Merchant registration foundation built. 🏪🔥**
