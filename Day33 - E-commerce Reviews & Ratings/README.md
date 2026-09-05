# Day 33 — Reviews & Ratings

## Overview

Day 33 focused on building a complete Reviews & Ratings system for the E-commerce API.

## Today's Work

- Built the Product Reviews & Ratings system
- Added review creation with purchase verification
- Implemented one-review-per-product protection
- Added review update and delete functionality with ownership security
- Implemented product reviews, average rating & total review calculation

## Review Features

### Create Review

- Only authenticated consumers can create reviews
- Consumers can review products they have purchased
- Only confirmed orders are considered eligible for reviews
- Validates product existence
- Supports ratings from 1 to 5
- Stores review comments

### Review Protection

- A consumer can only review the same product once
- Duplicate reviews are blocked
- Database-level unique compound index protects against duplicate reviews

### Update Review

- Consumers can update their own reviews
- Rating and comment can be updated independently
- Empty update requests are rejected
- Users cannot modify another user's review

### Delete Review

- Consumers can delete their own reviews
- Users cannot delete another user's review

### Product Reviews

- Get all reviews for a product
- Return reviewer name
- Sort reviews by newest first
- Validate product existence

### Product Rating

- Calculate average product rating dynamically
- Return total number of reviews
- Products without reviews return an average rating of `0` and total reviews of `0`
- Dynamic calculation keeps rating data consistent after review updates and deletions

## Validation

Zod validation was added for:

- Product ID
- Rating range
- Review comment length
- Review update fields
- At least one field required when updating

## Security

Review operations are protected using the existing authentication and authorization middleware.

- Consumer-only review creation, update, and deletion
- Authentication required for review modifications
- Ownership checks prevent users from modifying other users' reviews
- Purchased-product verification before review creation
- Product existence validation
- Duplicate review protection

## API Endpoints

### Reviews

POST `/api/reviews`

PATCH `/api/reviews/:reviewId`

DELETE `/api/reviews/:reviewId`

### Product Reviews

GET `/api/reviews/product/:productId`

### Product Rating

GET `/api/reviews/product/:productId/rating`

## Architecture

The Reviews feature follows the existing feature-based project structure:

```text
src/features/reviews/
├── review.model.js
├── review.service.js
├── review.controllers.js
├── review.routes.js
└── review.validation.js
```

The Review model references:

- `User` through `userId`
- `Product` through `productId`

Purchase verification uses the existing `Order` model.

Average ratings are calculated dynamically from the Review collection rather than being stored inside the Product model.

## Testing

- Review creation
- Confirmed purchased product verification
- Unpurchased product restriction
- Duplicate review protection
- Invalid rating validation
- Review update
- Review ownership protection
- Review deletion
- Product review retrieval
- Reviewer information
- Newest-first review sorting
- Average rating calculation
- Total review count
- Products with no reviews
- Authentication and authorization

## Repository

[E-commerce API](https://github.com/Greycode009/E-commerce-API)

## Day 33 Status

**Completed**
