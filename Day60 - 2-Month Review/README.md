# Day 60 — 2-Month Review

## Overview

Day 60 marked two months of the Becoming Better Developer journey.

Instead of adding a new feature, the day focused on reviewing and connecting the system design concepts learned throughout the previous days.

## What I Reviewed

- System design fundamentals
- Load balancing
- Health checks
- Redis caching
- Cache invalidation
- Redis failure handling
- MongoDB as the source of truth
- Horizontal scaling
- Failure scenarios

## Architecture Review

```text
User
  ↓
Load Balancer
  ↓
API Instances
  ↓
Redis
  ↓
MongoDB
```

### Request Flow

```text
User Request
    ↓
Load Balancer
    ↓
Healthy API Instance
    ↓
Check Redis
    ↓
Cache Hit?
 ├── YES → Return cached data
 └── NO
      ↓
   MongoDB
      ↓
   Store in Redis
      ↓
    Return data
```

## Failure Scenarios

### API Instance Failure

The Load Balancer uses health checks to detect unavailable API instances and routes requests to healthy instances.

### Redis Failure

Redis is treated as a performance layer rather than the source of truth.

```text
Redis Failure
     ↓
MongoDB
     ↓
Return Data
```

### MongoDB Failure

If the requested data is not already available in Redis, the API cannot retrieve fresh data and the request may fail.

## Key Lesson

The main focus of Day 60 was understanding how the individual backend concepts connect together to form a scalable and resilient architecture.

## Day 60 Complete

Completed two months of the Becoming Better Developer journey and strengthened understanding of the backend system architecture built throughout Days 1–59.
