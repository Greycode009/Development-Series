# Day 31 — Payment Flow

## Overview

Day 31 focused on implementing the core payment flow and connecting payments with the existing order system.

## Today's Work

- Built the Payment model
- Added payment validation with Zod
- Implemented payment creation
- Added order ownership protection
- Added duplicate payment protection
- Implemented payment status updates
- Added transaction ID generation for successful payments
- Automatically confirmed orders after successful payment
- Added consumer-only payment routes
- Tested successful, failed, invalid, duplicate, and unauthorized payment scenarios

## Payment Flow

```text
Consumer
   ↓
Create Payment
   ↓
Validate Order & Ownership
   ↓
Create Pending Payment
   ↓
Update Payment Status
   ↓
Paid
   ├── Generate Transaction ID
   └── Confirm Order
```

## Payment Status

- `pending`
- `paid`
- `failed`
- `refunded`

## Payment Methods

- `cod`
- `online`

## API Endpoints

### Create Payment

```http
POST /api/payments
```

Example body:

```json
{
  "orderId": "ORDER_ID",
  "method": "online"
}
```

### Update Payment Status

```http
PATCH /api/payments/:paymentId/status
```

Example body:

```json
{
  "status": "paid"
}
```

## Security

- Authentication is required for payment operations
- Only consumers can access payment endpoints
- Consumers can only access their own payments/orders
- Duplicate completed payments are prevented
- Payment amount is taken from the order subtotal instead of trusting the client

## Testing

- Successful payment
- Failed payment
- Invalid payment status
- Duplicate payment
- Unauthorized payment access
- Transaction ID generation
- Order confirmation after successful payment

## Repository

[E-commerce API](https://github.com/Greycode009/E-commerce-API)

## Day 31 Status

**Completed**
