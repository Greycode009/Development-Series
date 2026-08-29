# Day 26 — E-Commerce API: Merchant Onboarding & Authorization

## 📌 Overview

Today I continued building the **E-Commerce API** with Node.js, Express, MongoDB, and Mongoose.

The main focus was completing the **Merchant Onboarding and Authorization flow**, connecting merchant accounts with the existing authentication system, and securing merchant product management.

---

## Project Repository

🔗 [E-commerce API — GitHub](https://github.com/Greycode009/E-commerce-API.git)

---

## 🚀 What I Built

### 🔐 Merchant OTP Verification

Connected merchant registration with the existing OTP verification system.

The same OTP system is now reused for both consumers and merchants.

```text
Merchant Registration
        ↓
Create Merchant User
        ↓
Generate OTP
        ↓
Hash OTP
        ↓
Send OTP
        ↓
Verify OTP
        ↓
verified: true
```

### 🔑 Single Login System

Kept the existing single login system for all users.

Consumers and merchants use the same login endpoint. The authenticated user's role is used to determine access.

```text
Login
  ↓
Authenticate
  ↓
Identify role
  ↓
consumer / merchant / admin
```

The frontend can display the appropriate dashboard:

```text
consumer → Consumer Dashboard
merchant  → Merchant Dashboard
admin     → Admin Dashboard
```

### 🛡️ Merchant Authorization

Implemented role-based protection for merchant functionality.

Merchant routes use:

```text
authenticate
     ↓
authorize("merchant")
```

Example:

```text
Merchant → /api/merchant/profile → 200 ✅
Consumer → /api/merchant/profile → 403 ❌
```

### 🏪 Merchant Profile API

Added a protected merchant profile endpoint:

```text
GET /api/merchant/profile
```

The authenticated merchant's ID is taken from:

```js
req.user.id
```

The API retrieves the merchant profile associated with that user.

### 🛒 Merchant Product Management

Connected the existing Product system with authenticated merchants.

When a merchant creates a product, the merchant ID is automatically assigned from the authenticated user:

```js
merchant: req.user.id
```

The client does not control product ownership.

```text
Merchant Login
      ↓
JWT
      ↓
req.user.id
      ↓
Create Product
      ↓
merchant = req.user.id
```

### 🔒 Product Ownership Protection

Added ownership checks for product updates and deletion.

A merchant can only modify or delete products that belong to them.

The update and delete queries check both the product ID and authenticated merchant ID:

```js
{
    _id: id,
    merchant: merchantId
}
```

Therefore:

```text
Merchant A → Own Product → Update/Delete ✅

Merchant B → Merchant A's Product → Blocked ✅
```

This prevents one merchant from modifying another merchant's products.

### 🌐 Product Route Authorization

Product access was separated based on the operation.

Public:

```text
GET /api/products
GET /api/products/:id
```

Merchant-only:

```text
POST /api/products
PUT /api/products/:id
DELETE /api/products/:id
```

Merchant management routes require authentication and the `merchant` role.

---

## 🧪 Testing

Tested the merchant authentication, authorization, product management, and ownership flows.

### Merchant

- Merchant registration ✅
- OTP verification ✅
- Merchant login ✅
- Merchant profile access ✅
- Merchant product creation ✅
- Merchant can update own product ✅
- Merchant can delete own product ✅

### Authorization

- Consumer blocked from merchant profile ✅
- Consumer blocked from creating products ✅
- Merchant-only routes protected ✅

### Ownership

- Merchant can modify own product ✅
- Merchant cannot modify another merchant's product ✅
- Merchant cannot delete another merchant's product ✅

---

## 🧠 Concepts Reinforced

- JWT authentication
- Role-based authorization
- Authentication middleware
- `req.user`
- Protected routes
- Feature-based architecture
- Merchant-product relationships
- Mongoose ObjectId references
- Resource ownership
- Server-side ownership assignment
- `findOneAndUpdate()`
- `findOneAndDelete()`
- API security
- Access control testing

---

## 📌 Current Architecture

```text
                    E-COMMERCE API
                           │
                    Single Login
                           │
                    Authenticate
                           │
                      Check Role
                 ┌─────────┼─────────┐
                 ↓         ↓         ↓
             Consumer   Merchant    Admin
                 │         │         │
                 ↓         ↓         ↓
             Consumer   Merchant    Admin
             Features   Features   Features
```

Merchant product flow:

```text
Merchant
   ↓
Authenticate
   ↓
Authorize("merchant")
   ↓
Create Product
   ↓
Product → merchant: req.user.id
```

---

## 📊 Current Status

### Authentication

**Complete ✅**

### Merchant Registration

**Complete ✅**

### Merchant OTP Verification

**Complete ✅**

### Merchant Authorization

**Complete ✅**

### Merchant Product Management

**Complete ✅**

### Product Ownership Protection

**Complete ✅**

---

## 🔜 Next

Continue expanding the E-Commerce API with the next feature while keeping the existing authentication, authorization, and ownership patterns.

---

**Day 26 complete. Merchant onboarding and authorization secured. 🏪🔐🔥**
