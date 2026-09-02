# Day 30 — Order Management & Order History

Repository: https://github.com/Greycode009/E-commerce-API

## Day 30 Progress

- Implemented consumer order history
- Added secure order details with ownership protection
- Added merchant-specific order management
- Implemented merchant order status updates
- Added consumer order cancellation with stock restoration

## Features

### Consumer Order History
Consumers can retrieve their own orders, sorted newest first.

### Order Details
Consumers can retrieve a specific order while ownership is verified.

### Merchant Order Management
Merchants can retrieve orders containing their products using `merchantId` stored in OrderItems.

### Order Status
Merchants can update order status. Current statuses:
- pending
- confirmed
- cancelled

### Consumer Cancellation
Consumers can cancel their own orders only while they are `pending`. Product stock is restored and the cancelled order remains stored for order history.

## API Endpoints

```text
GET   /api/orders/my-orders
GET   /api/orders/:orderId
GET   /api/orders/merchant
PATCH /api/orders/:orderId/status
PATCH /api/orders/:orderId/cancel
```

## Security

- Consumer-only access for order history and cancellation
- Merchant-only access for merchant order management
- Order ownership validation
- Merchant-specific order filtering
- Protected status updates

## Testing

- Consumer order history
- Individual order details
- Consumer ownership protection
- Merchant order access
- Merchant-specific order filtering
- Merchant status update
- Unauthorized merchant access
- Consumer order cancellation
- Stock restoration after cancellation

## Result

Day 30 completes the core Order Management and Order History functionality, connecting consumers and merchants through the order lifecycle.
