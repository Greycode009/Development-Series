# Day 29 — E-commerce Orders & Checkout

## Overview

---

## Project Repository

🔗 [E-commerce API — GitHub](https://github.com/Greycode009/E-commerce-API.git)

---

Day 29 focused on building the Order and Checkout system for the E-commerce API.

- Created Order and OrderItem models
- Implemented Cart → Checkout → Order workflow
- Added product and stock validation during checkout
- Stored product price at the time of purchase
- Reduced product stock and cleared the cart after successful checkout
- Tested successful, empty-cart, and insufficient-stock checkout flows

## Order System

The Order model stores the authenticated consumer, ordered products, quantity, purchase-time price, product image, subtotal, and order status.

Initial order statuses:

```text
pending
confirmed
cancelled
```

## Checkout Flow

```text
Consumer
   ↓
Cart
   ↓
Checkout
   ↓
Validate Cart
   ↓
Validate Products & Stock
   ↓
Create Order
   ↓
Reduce Product Stock
   ↓
Clear Cart
   ↓
Order Created
```

## Checkout API

```http
POST /api/orders
```

The endpoint is protected using authentication and consumer-only authorization.

No request body is required because the order is created from the authenticated consumer's cart.

## Price Snapshot

The product price is copied from the cart into the OrderItem.

This preserves the price at the time of purchase even if the merchant changes the product price later.

## Stock Handling

Before creating an order, the system checks that the product exists and that the requested quantity is available.

After a successful order, product stock is reduced according to the ordered quantity.

## Cart Handling

After successful checkout:

```text
items → []
subtotal → 0
```

The Cart document remains associated with the authenticated consumer.

## Testing

Tested:

- Successful checkout
- Order creation
- Product stock reduction
- Cart clearing after checkout
- Empty cart checkout
- Insufficient stock checkout
- Consumer authentication and authorization

## Concepts Reinforced

- Order and OrderItem modeling
- Checkout business logic
- Stock validation
- Inventory reduction
- Price snapshotting
- Authentication
- Role-based authorization
- Cart-to-order conversion
- API testing

## Result

The core Cart → Checkout → Order flow is now working successfully.

## Next

Continue with Order Management and Order History.

---

**Day 29 complete. Orders & Checkout implemented.**
