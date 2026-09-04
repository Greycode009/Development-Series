# Backend Learning Summary

## Day 1 - Authentication

- Set up a basic Express/MongoDB authentication flow
- Implemented user registration and login
- Stored hashed passwords in MongoDB
- Added JWT access token generation
- Built auth routes and controller logic

## Day 2 - Authentication

- Added refresh token handling and session storage
- Implemented secure HTTP-only refresh cookies
- Added `getMe`, `refreshToken`, `logout`, and `logoutAll` routes
- Created session persistence with refresh token hashing
- Improved auth flow with token rotation and revocation support

## Day 3 - Complete Authentication

- Added email verification with OTP generation and verification
- Implemented email delivery using Nodemailer and Gmail OAuth2
- Added OTP storage, expiration, and validation in MongoDB
- Enforced email verification before login
- Added rollback on failed email send and improved error handling
- Continued managing access/refresh tokens and session logout

## Day 4 - Authorization

- Implemented JWT authentication middleware (`VerifyJWT`) to protect private routes
- Built Role-Based Access Control (RBAC) using user roles and authorization middleware
- Added role information to JWT access tokens for permission-based route protection
- Implemented session validation to revoke access after logout or session expiration
- Secured protected routes with authentication and authorization middleware chaining
- Learned the concept of Ownership-Based Authorization for resource-level access control

## Day 5 – Blog API

- Started building a **Blog API** with Node.js & MongoDB
- Integrated **Authentication & Authorization**
- Implemented **Protected & Role-Based Routes**
- Built **Create & Read Blog APIs**
- Connected blogs with **authenticated users & ownership**

## Day 6 - Blog API & CRUD

- Built Complete Blog CRUD APIs
- Implemented Ownership-Based Access Control
- Connected Blogs with User Accounts
- Tested All CRUD Operations with Postman
- Verified Authorization, Error Handling & Edge Cases

## Day 7 - Comment API

- Built a complete **Comment CRUD API**
- Connected Comments with **Users & Blogs**
- Implemented **Comment Ownership Authorization**
- Added **Blog Existence Validation**
- Tested Comment CRUD, Authorization & **Edge Cases**

## Day 8 - Request Validation

- Added Zod for request validation
- Created reusable validation middleware
- Added Blog & Comment validation schemas
- Validated Create & Update API requests
- Tested valid, invalid, and edge-case inputs

## Day 9 - Centralized Error Handling

- Learned **Centralized Error Handling** in Express
- Created a reusable **`AppError`** class with status codes
- Implemented **Global Error Handling Middleware**
- Learned to handle **404, 403, 400 (CastError), and 500 errors**
- Integrated **Zod validation errors** with the centralized error system

## Day 10 - Pagination

- Learned **API Pagination** with `page` and `limit`
- Implemented MongoDB **`skip()` & `limit()`**
- Added **pagination metadata** with total pages
- Added **Zod validation** for query parameters
- Implemented reusable validation for **body & query** data

## Day 11 - Search, Filtering & Sorting

- Implemented **Blog Search** using title & content
- Added **Author Filtering**
- Added **Latest & Oldest Sorting**
- Combined **Search, Filter & Sort with Pagination**
- Tested **Individual & Combined Queries**

## Day 12 - Practice & Revisit

- Revisited **Search, Filtering, Sorting & Pagination**
- Practiced **Combined Query Parameters**
- Tested **Complex API Queries**
- Debugged **Pagination Logic**
- Reviewed **Request → Controller → Service → Database** flow

## Day 13 - Blog API Frontend Integration

- Built and integrated the **Blog API frontend**
- Connected the frontend with the **backend REST API**
- Implemented **All Stories & My Stories**
- Added **Search, Sorting & Pagination** to the frontend
- Connected **Author Filtering** through My Stories
- Tested the complete **Frontend → Backend → Database → Frontend** flow

## Day 14 - URL Shortener Design

- Started the **URL Shortener Project**
- Designed the **API Requirements & Endpoints**
- Defined the **URL Data Model**
- Planned the **Short-Code Generation Strategy**
- Designed the **Short URL Creation & Redirect Flow**

## Day 15 - Short URL Creation

- Built the **Short URL Creation API**
- Added **URL Validation**
- Implemented **6-Character Short-Code Generation**
- Connected **Sequelize with PostgreSQL**
- Added **Unique Short-Code Collision Handling**
- Tested the complete **Request → Controller → Service → Database** flow

## Day 16 - Short URL Redirection

- Built the **Short URL Redirect API**
- Added **Short-Code Lookup & 404 Handling**
- Implemented **Redirect to Original URL**
- Tested the complete **Request → Controller → Database → Redirect** flow
- Committed and pushed the completed **Day 16 progress**

## Day 17 - Click Tracking & Analytics

- Added **Click Tracking** for Short URLs
- Added **Click Count** to the URL model
- Implemented **Automatic Click Increment** on redirects
- Built the **URL Statistics Endpoint**
- Tested the complete **Redirect → Click Tracking → Statistics** flow

## Day 18 - URL Shortener Production Features

- Added **URL Expiration** with expiry-date validation
- Implemented **Expired URL Handling** with `410 Gone`
- Added **Rate Limiting** using `express-rate-limit`
- Added **Custom Short Code** support with validation and duplicate protection
- Tested **Edge Cases & Production Scenarios**

## Day 19 — File Uploads 🚀

- Learned **`multipart/form-data`** and how file uploads differ from JSON
- Implemented **Multer single-file uploads**
- Added **image type & 2 MB size validation**
- Built **upload error handling** with clean JSON responses
- Organized the upload feature using **routes, controllers & middleware** and tested the complete flow

## Day 20 — Cloud Image Uploads ☁️

- Learned **cloud storage** for backend file uploads
- Used **Multer `memoryStorage()`**
- Uploaded images directly to **Supabase Storage**
- Generated and used **public image URLs**
- Built a reusable **Node.js + Supabase upload flow**

## Day 21 — File Management ☁️

- Implemented **single-file deletion** from Supabase Storage
- Added **multiple-file deletion** using batch operations
- Built reusable **file management services**
- Debugged and fixed **Supabase Storage API errors** 🛠️

## Day 22 — E-commerce API 🛒

- Designed the E-commerce API architecture
- Defined Consumer, Merchant, and Super Admin roles
- Designed Product, Cart, Order, and Inventory systems
- Set up MongoDB Atlas with Mongoose
- Built the Product model
- Implemented the Product creation API

## Day 23 — E-commerce Product CRUD & Cart

- Completed Product CRUD APIs
- Implemented Zod validation
- Implemented `AppError` and Global Error Handler
- Added proper 404 and invalid ObjectId error handling
- Refactored controllers to use centralized error handling
- Built Cart and CartItem schemas
- Implemented Get Cart API
- Implemented Add-to-Cart business logic
- Added stock and duplicate-item handling
- Implemented dynamic cart subtotal calculation
- Tested APIs and committed changes

## Day 24 — E-commerce Authentication and Authorization

- Implemented User model with roles and verification status
- Implemented user registration with Argon2id password hashing
- Implemented OTP-based email verification
- Added OTP hashing and 10-minute expiration with TTL index
- Implemented OTP resend functionality
- Implemented login with JWT access and refresh tokens
- Added session management for refresh tokens
- Stored refresh tokens in HTTP-only cookies
- Implemented access token refresh
- Implemented logout and logout from all devices
- Implemented authentication middleware and attached authenticated user to `req.user`
- Implemented role-based authorization for consumer, merchant, and admin
- Tested authentication and authorization flows
- Committed changes and created Pull Request
- Reviewed, merged PR, and deleted feature branch

## Day 25 — E-commerce Merchant Registration

- Created Merchant feature structure and model
- Implemented merchant registration flow
- Added merchant registration validation
- Added pending merchant approval status
- Implemented merchant registration API
- Secured registration response by removing password
- Tested merchant registration successfully

## Day 26 — E-commerce Merchant Onboarding & Authorization

- Implemented merchant OTP verification
- Added merchant role-based authorization
- Built protected merchant profile API
- Connected products with authenticated merchants
- Added merchant product ownership protection
- Tested merchant and consumer access
- Tested cross-merchant product protection
- Committed, merged PR, and deleted feature branch

## Day 27 — E-commerce Cart Authentication & User Integration

- Replaced temporary `consumerId` with authenticated `userId`
- Updated Cart ownership to use the authenticated user
- Added consumer-only Cart authorization
- Updated Cart services to use `req.user.id`
- Tested Cart access, Add-to-Cart, and authorization
- Tested complete Merchant → Product → Consumer → Cart flow

## Day 28 — E-commerce Cart Management

- Implemented cart item quantity update
- Added quantity and stock validation
- Implemented individual cart item removal
- Implemented clear cart functionality
- Added dynamic subtotal recalculation
- Completed and tested the full Cart management flow

## Day 29 — E-commerce Orders & Checkout

- Created Order and OrderItem models
- Implemented Cart → Checkout → Order workflow
- Added product and stock validation
- Added purchase-time price snapshotting
- Implemented stock reduction and automatic cart clearing

## Day 30 — Order Management & Order History

- Implemented consumer order history
- Added secure order details with ownership protection
- Added merchant-specific order management
- Implemented merchant order status updates
- Added consumer order cancellation with stock restoration

## Day 31 — Payment Flow

- Built the Payment System
- Added Payment Validation with Zod
- Implemented Payment Creation & Ownership Protection
- Added Payment Status & Transaction ID
- Connected Successful Payment → Order Confirmation

## Day 32 - Admin Management

- Built the Admin Management System
- Added Admin User & Merchant Management
- Implemented Admin Order Management
- Added User Activate / Deactivate & Delete
- Added Admin Security & Authorization Testing