# E-commerce API — Complete Design 🛒

## 1. Roles

Our E-commerce API will have **3 roles**:

### Consumer 🛍️
- Browse products
- Search and filter products
- Manage their own cart
- Place orders
- View and manage their own orders

### Merchant 🏪
- Create products
- Update their own products
- Delete their own products
- Manage their inventory
- View orders related to their products

### Super Admin 👑
- Manage consumers
- Manage merchants
- Manage all products
- Manage categories
- Manage all orders
- Manage platform-level data

### Authorization

A merchant can only manage **their own products**.

A consumer can only access **their own cart and orders**.

A super admin can access and manage everything.

---

# 2. Product Design 📦

```text
Product
├── title
├── description
├── price
├── stock
├── category
├── merchant
├── imageUrl
├── createdAt
└── updatedAt
```

### Product Rules

- `title` is required
- `description` is required
- `price` cannot be negative
- `stock` cannot be negative
- Product belongs to a merchant
- Merchant can only modify their own products
- `createdAt` and `updatedAt` are automatically managed

For the initial version, we are keeping the product simple and **not adding** SKU, GTIN, MPN, SEO data, dimensions, warehouse locations, etc.

---

# 3. Cart Design 🛒

A consumer has a cart containing products and quantities.

```text
Cart
├── cart_id
├── consumer
├── items
│   ├── product_id
│   ├── title
│   ├── quantity
│   ├── price
│   └── image_url
├── subtotal
├── coupon_code
├── createdAt
└── updatedAt
```

### Cart Rules

- Only the consumer who owns the cart can manage it
- Quantity must be greater than `0`
- Product must exist
- Quantity cannot exceed available stock
- The same product should not appear as separate cart items
- Cart items reference actual products
- Subtotal is calculated from product price × quantity
- Coupon codes can later be used for discount logic

We are keeping the initial cart design simple and **not adding product variants such as size/color yet**.

---

# 4. Order Design 📦

An order is created when a consumer checks out.

```text
Cart
  ↓
Checkout
  ↓
Order
```

```text
Order
├── order_id
├── consumer
├── items
│   ├── product_id
│   ├── title
│   ├── price
│   └── quantity
├── subtotal
├── discount
├── total
├── status
├── createdAt
└── updatedAt
```

### Order Status

```text
pending
   ↓
confirmed
   ↓
shipped
   ↓
completed
```

Orders can also be:

```text
pending → cancelled
confirmed → cancelled
```

### Order Rules

- Consumer can only view their own orders
- An order must contain at least one item
- Products must exist
- Backend calculates the order total
- Stock must be checked before creating the order
- Consumer cannot randomly change the order status
- Only authorized roles can manage order status
- Order should preserve the price and product information at checkout

### Why preserve product information?

If a product costs `$25` when purchased and later changes to `$30`, the old order should still show `$25`.

The historical order should not change when the product changes.

---

# 5. Inventory Design 📊

For the initial version, we will **not create a separate Inventory model**.

Inventory will be represented by:

```text
Product.stock
```

### Inventory Rules

- Stock cannot be negative
- Order quantity must be greater than `0`
- Order quantity cannot exceed available stock
- Successful orders reduce product stock
- Failed orders must not reduce stock

### Race Condition

Example:

```text
Stock = 1

Consumer A → buys 1
Consumer B → buys 1
```

Both requests should **not** successfully purchase the same final item.

We will later handle this with:

- Safe stock updates
- Database transactions
- Data consistency
- Race-condition handling

---

# 6. Main Relationships 🔗

```text
User
├── Consumer
├── Merchant
└── Super Admin
```

```text
Merchant
   ↓
owns
   ↓
Products
```

```text
Consumer
   ↓
owns
   ↓
Cart
```

```text
Cart
   ↓
contains
   ↓
Cart Items
   ↓
Products
```

```text
Consumer
   ↓
creates
   ↓
Orders
```

```text
Order
   ↓
contains
   ↓
Order Items
   ↓
Products
```

Overall:

```text
Merchant
   │
   └── Products
          │
          └── Stock

Consumer
   │
   ├── Cart
   │     └── Cart Items → Products
   │
   └── Orders
         └── Order Items → Products
```

---

# 7. Main Business Flow 🛍️

```text
Merchant
   ↓
Creates Product
   ↓
Product available
   ↓
Consumer browses products
   ↓
Consumer adds product to Cart
   ↓
Consumer checks out
   ↓
Check product stock
   ↓
Calculate total
   ↓
Create Order
   ↓
Reduce Product stock
   ↓
Order created
```

---

# 8. Initial API Design

## Products

```text
POST   /api/products
GET    /api/products
GET    /api/products/:id
PUT    /api/products/:id
DELETE /api/products/:id
```

## Cart

```text
GET    /api/cart
POST   /api/cart/items
PATCH  /api/cart/items/:productId
DELETE /api/cart/items/:productId
```

## Orders

```text
POST   /api/orders
GET    /api/orders
GET    /api/orders/:id
PATCH  /api/orders/:id/status
```

These routes will be refined as we implement the project and discover the exact requirements.

---

# 9. Future Performance & Production Features ⚡

We will introduce these when the project actually gives us a reason to use them.

### Redis & Caching

```text
GET /products
       ↓
   Redis Cache?
    ↙       ↘
  HIT       MISS
   ↓          ↓
 Return    MongoDB
              ↓
           Redis
              ↓
           Return
```

We'll learn:

- Redis
- Cache keys
- TTL
- Cache-aside pattern
- Cache invalidation
- Query optimization

### Transactions

For checkout:

```text
Create Order
     +
Reduce Stock
```

These operations should remain consistent.

### Background Jobs

If the project needs asynchronous work later:

```text
API
 ↓
Queue
 ↓
Worker
 ↓
Background task
```

### Docker

Later we'll containerize the application and supporting services when the project becomes complex enough to benefit from it.

---

# 10. Project Architecture

We will use a **feature-based structure**:

```text
src/
├── config/
├── middleware/
│
├── features/
│   ├── products/
│   │   ├── product.model.js
│   │   ├── product.service.js
│   │   ├── product.controller.js
│   │   └── product.routes.js
│   │
│   ├── carts/
│   └── orders/
│
├── app.js
└── server.js
```

We are using:

```text
Node.js
Express.js
MongoDB
Mongoose
Zod
```

Redis, caching, queues, Docker, and other production technologies will be introduced when the project needs them.

---

# 11. Learning Approach

We will follow:

```text
Understand
    ↓
Implement
    ↓
Test
    ↓
Break
    ↓
Fix
    ↓
Explain
    ↓
Reuse
    ↓
Move on
```

We will **not stretch the project just to fill days**.

The goal is to understand how an e-commerce backend actually works and gradually become able to build the features independently.

---

# Current Status — Day 22

```text
Project Design          ✅
Roles                   ✅
Product Design          ✅
Cart Design             ✅
Order Design            ✅
Inventory Design        ✅
MongoDB Atlas Setup     ✅
Product Model           ✅
Product Creation API    ✅
```

**Next:** Product validation → Product listing → Product management.
