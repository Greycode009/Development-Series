# Day 32 — Admin Management

## Overview

Day 32 focused on building the Admin Management system for the E-commerce API.

## Today's Work

- Built the Admin Management System
- Added Admin User & Merchant Management
- Implemented Admin Order Management
- Added User Activate / Deactivate & Delete
- Added Admin Security & Authorization Testing

## Admin Features

### User Management

- View all users
- View individual users
- Activate users
- Deactivate users
- Permanently delete users
- Prevent deactivated users from logging in

### Merchant Management

- View all merchants
- View individual merchant details
- Populate merchant account information from the User model

### Order Management

- View all orders
- View individual order details
- Sort orders by newest first

## Security

Admin operations are protected using the existing authentication and authorization middleware.

- Admin-only access
- Consumer access blocked
- Merchant access blocked
- Unauthenticated access blocked
- Deactivated users cannot log in
- User passwords are not exposed in admin responses

## API Endpoints

### Users

```http
GET /api/admin/users
GET /api/admin/users/:userId
PATCH /api/admin/users/:userId/status
DELETE /api/admin/users/:userId
```

### Merchants

```http
GET /api/admin/merchants
GET /api/admin/merchants/:merchantId
```

### Orders

```http
GET /api/admin/orders
GET /api/admin/orders/:orderId
```

## Architecture

Admin accounts use the existing `User` model with:

```text
role: "admin"
```

Merchants are also users with:

```text
role: "merchant"
```

Merchant-specific business information is stored separately in the `Merchant` model and connected through `userId`.

## Testing

- Admin access
- Consumer access restriction
- Merchant access restriction
- Unauthenticated access restriction
- Get all users
- Get individual user
- Get all merchants
- Get individual merchant
- Get all orders
- Get individual order
- User deactivation
- User reactivation
- Login prevention for deactivated users
- User deletion

## Repository

[E-commerce API](https://github.com/Greycode009/E-commerce-API)

## Day 32 Status

**Completed**
