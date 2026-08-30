# Day 28 — E-Commerce API: Cart Management

## 📌 Overview

Today I continued building the **E-Commerce API** with Node.js, Express, MongoDB, and Mongoose.

The main focus was improving the **Cart Management system** and adding the functionality required for consumers to manage items in their cart.

---

## Project Repository

🔗 [E-commerce API — GitHub](https://github.com/Greycode009/E-commerce-API.git)

---

## 🚀 What I Built

### 🛒 Update Cart Item Quantity

Implemented functionality to update the quantity of an existing cart item.

Added:

- Quantity validation
- Stock validation
- Dynamic subtotal recalculation

---

### 📦 Stock & Quantity Validation

Added validation to ensure cart quantities remain valid and do not exceed the available product stock.

```text
Requested Quantity
        ↓
Check Product Stock
        ↓
Valid → Update Cart
Invalid → Return Error
```

---

### 🗑️ Remove Cart Item

Implemented functionality to remove a specific product from the authenticated consumer's cart.

After removing an item, the cart subtotal is recalculated automatically.

---

### 🧹 Clear Cart

Implemented functionality to clear all items from the authenticated consumer's cart.

After clearing:

```text
items → []
subtotal → 0
```

---

### 💰 Dynamic Cart Subtotal

The cart subtotal is recalculated whenever cart contents change.

```js
cart.items.reduce(
  (total, item) => total + item.price * item.quantity,
  0
);
```

This keeps the subtotal synchronized after quantity updates, item removal, and clearing the cart.

---

## 🔐 Cart Security

Cart management continues to use the existing authentication and authorization system.

```text
authenticate
      ↓
authorize("consumer")
      ↓
Cart operation
```

The authenticated user's ID is used to identify the cart, preventing users from managing another user's cart.

---

## 🧪 Testing

Tested the main Cart management flows:

- Update cart item quantity ✅
- Quantity validation ✅
- Stock validation ✅
- Remove cart item ✅
- Clear cart ✅
- Dynamic subtotal calculation ✅
- Consumer-only Cart access ✅

---

## 🧠 Concepts Reinforced

- Cart management
- Mongoose embedded documents
- Array manipulation
- Quantity validation
- Stock validation
- Resource ownership
- Authentication and authorization
- Dynamic calculations
- Business logic separation
- API testing

---

## 📊 Current Cart System

```text
Consumer
   ↓
Authenticated Cart
   ↓
┌────────────────────┐
│ Add Item            │
│ Get Cart            │
│ Update Quantity     │
│ Remove Item         │
│ Clear Cart          │
└────────────────────┘
```

---

## 📌 Current Status

### Cart Management

**Complete ✅**

### Quantity & Stock Validation

**Complete ✅**

### Remove Cart Item

**Complete ✅**

### Clear Cart

**Complete ✅**

### Dynamic Subtotal

**Complete ✅**

---

## 🔜 Next

Continue expanding the E-Commerce API with the next major feature while keeping the existing authentication, authorization, product, and cart architecture.

---

**Day 28 complete. Cart management system improved. 🛒🔥**
