# Day 59 — Caching Strategy

## Project

**E-commerce API**

Repository: https://github.com/Greycode009/E-commerce-API

## What I Learned

Day 59 focused on understanding and improving the caching strategy using Redis.

### Topics Covered

- Cache-aside pattern
- Cache hit and cache miss
- Cache key design
- TTL and cache expiration
- Cache invalidation
- Redis failure handling
- MongoDB fallback
- Redis as a performance layer

## Cache Flow

```text
Client
  ↓
API Server
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
    Return
```

## Redis Failure Handling

Redis should improve performance but should not become a required dependency for the API.

```text
Redis Available
      ↓
Use Cache
      ↓
Fast Response
```

If Redis is unavailable:

```text
Redis Failure
     ↓
Ignore Cache Failure
     ↓
MongoDB
     ↓
Return Data
```

## Improvements

- Protected Redis cache reads with `try/catch`
- Protected Redis cache writes with `try/catch`
- Made cache invalidation resilient to Redis failures
- Made rate limiting continue when Redis is unavailable
- Kept MongoDB as the source of truth

## Testing

Tested the system with Redis running:

```text
CACHE MISS → MongoDB → Redis
CACHE HIT  → Redis
```

Tested with Redis stopped:

```text
Redis unavailable
      ↓
MongoDB
      ↓
API still works
```

Also verified:

- Product retrieval
- Product update/delete
- Cache invalidation
- API rate limiting

## Key System Design Lesson

> Redis is a performance layer, not the source of truth.

A cache failure should reduce performance, not bring down the entire API.

## Day 59 Complete

Improved the Redis caching strategy and learned how to design a more resilient caching layer for a scalable backend.
