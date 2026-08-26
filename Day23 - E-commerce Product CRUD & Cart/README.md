# Day 23 — E-Commerce API: Product CRUD & Cart

## 📌 Overview

Today I continued building the **E-Commerce API** with Node.js, Express, MongoDB, and Mongoose.

The main focus was completing the **Product CRUD system**, implementing **global error handling**, and starting the **Cart system**.

---

## Project Repository

🔗 [E-commerce API — GitHub](https://github.com/Greycode009/E-commerce-API.git)

## 🚀 What I Built

### 🏪 Product API

Completed the full Product CRUD:

- `POST /api/products` — Create Product
- `GET /api/products` — Get All Products
- `GET /api/products/:id` — Get Single Product
- `PUT /api/products/:id` — Update Product
- `DELETE /api/products/:id` — Delete Product

### ✅ Product Validation

Implemented Zod validation for product creation and updates.

Validated:

- Title
- Description
- Price
- Stock
- Category
- Image URL

---

## 🚨 Global Error Handling

Revisited and implemented the **Global Error Handler** that I previously learned.

### Added

- `AppError`
- Global error middleware
- Product not found → `404`
- Invalid MongoDB ObjectId → `400`
- Centralized unexpected error handling

Example:

```text
/products/abc
      ↓
Mongoose CastError
      ↓
Global Error Handler
      ↓
400 Invalid ID format
```

---

## 🛒 Cart System

Started building the Cart module.

### Cart Model

Created:

- `Cart` schema
- `CartItem` embedded schema
- Consumer ID
- Cart items
- Subtotal
- Coupon code
- Timestamps

Cart items contain:

- Product ID
- Title
- Quantity
- Price
- Image URL

### Cart API

Started:

```text
GET  /api/cart/:consumerId
POST /api/cart/:consumerId/items
```

### Add-to-Cart Business Logic

Implemented:

- Product existence check
- Stock validation
- Find or create cart
- Prevent duplicate cart items
- Increase quantity for existing items
- Add new products to cart
- Dynamic subtotal calculation
- Save updated cart

Subtotal is calculated using:

```js
cart.items.reduce((total, item) => total + item.price * item.quantity, 0);
```

---

## 🧠 Concepts Reinforced

- Controller vs Service responsibilities
- Custom error classes
- Global error handling
- Mongoose `CastError`
- Embedded Mongoose schemas
- `reduce()` for calculations
- Request validation vs business logic
- MongoDB ObjectIds
- Cart business logic

---

## 📌 Current Status

### Product

**CRUD Complete ✅**

### Cart

**Foundation + Add-to-Cart logic 🚧**

Authentication and Consumer/User system are not implemented yet, so Cart currently uses a temporary `consumerId`.

---

## 🔜 Next — Day 24

### Authentication

- User/Consumer model
- Registration
- Password hashing
- Login
- JWT
- Authentication middleware
- `req.user`
- Role-based authorization

Then authentication will be connected properly with the Cart system.

---

**Day 23 complete. 🛒🔥**
