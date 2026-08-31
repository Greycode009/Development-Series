# Day 28 — E-commerce Cart Management

## 📌 Overview

Day 28 focused on completing the Cart Management system of the E-commerce API.

The existing authenticated Cart system was extended so consumers can fully manage items in their cart while maintaining stock validation, ownership, authorization, and accurate subtotal calculations.

---

## Project Repository

🔗 [E-commerce API — GitHub](https://github.com/Greycode009/E-commerce-API.git)

---

## 🎯 Objectives

- Update cart item quantities
- Validate quantity and product stock
- Remove individual cart items
- Clear the entire cart
- Recalculate the cart subtotal dynamically
- Keep Cart operations restricted to authenticated consumers

---

## 🛒 Features Implemented

### Update Cart Item Quantity

Implemented an API for updating the quantity of an existing cart item.

The system finds the authenticated consumer's cart, verifies the item exists, validates the requested quantity and product stock, updates the quantity, and recalculates the subtotal.

```text
Gaming Mouse × 2
Subtotal: 6800

Update quantity → 3

Gaming Mouse × 3
Subtotal: 10200
```

### Quantity & Stock Validation

Added validation to prevent invalid quantities and quantities greater than the available product stock.

```text
Requested Quantity
        ↓
Validate Quantity
        ↓
Check Product Stock
        ↓
Valid → Update Cart
Invalid → Return Error
```

### Remove Individual Cart Item

Implemented:

```http
DELETE /api/cart/items/:productId
```

The selected item is removed from the authenticated consumer's cart and the subtotal is recalculated.

### Clear Cart

Implemented:

```http
DELETE /api/cart
```

All items are removed while the Cart document remains associated with the authenticated consumer.

```text
items → []
subtotal → 0
```

---

## 💰 Dynamic Subtotal

The subtotal is recalculated whenever cart contents change.

```js
cart.subtotal = cart.items.reduce(
  (total, item) => total + item.price * item.quantity,
  0
);
```

This keeps the subtotal accurate after quantity updates, item removal, and clearing the cart.

---

## 🔐 Authorization & Ownership

Cart management uses the existing authentication and authorization system.

```text
authenticate
      ↓
authorize("consumer")
      ↓
Cart operation
```

The authenticated user's ID is used to identify the Cart:

```js
req.user.id
```

This ensures consumers can only manage their own Cart.

---

## 🌐 Cart API

```text
GET    /api/cart
POST   /api/cart/items
PATCH  /api/cart/items/:productId
DELETE /api/cart/items/:productId
DELETE /api/cart
```

Access:

```text
Consumer          → Cart operations ✅
Merchant          → Cart operations ❌
Unauthenticated   → Cart operations ❌
```

---

## 🧪 Testing

The following Cart flows were tested:

- Update cart item quantity ✅
- Quantity validation ✅
- Stock validation ✅
- Remove individual cart item ✅
- Clear Cart ✅
- Dynamic subtotal recalculation ✅
- Consumer Cart authorization ✅
- Merchant access restriction ✅
- Unauthenticated access restriction ✅
- Empty Cart behavior ✅
- Complete Cart management flow ✅

---

## 🧠 Concepts Reinforced

- Cart management
- Mongoose embedded documents
- Array manipulation
- Quantity validation
- Stock validation
- Authentication middleware
- Role-based authorization
- Resource ownership
- Dynamic calculations
- Business logic separation
- API testing

---

## 📊 Day 28 Result

The Cart system is now a complete authenticated feature:

```text
Consumer Login
      ↓
Authenticated User
      ↓
Cart
      ↓
┌──────────────────────┐
│ Get Cart             │
│ Add Product          │
│ Update Quantity      │
│ Remove Item          │
│ Clear Cart           │
└──────────────────────┘
      ↓
Dynamic Subtotal
```

---

## 🔜 Next

The Cart system is complete and ready for the next major E-commerce feature:

**Orders & Checkout 📦**

---

**Day 28 complete. Cart management system completed. 🛒🔥**
