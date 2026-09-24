# Day 52 - Redis Product Caching

## Project

**E-commerce API**

Repository: https://github.com/Greycode009/E-commerce-API

## Overview

On Day 52, I started learning Redis and integrated Redis caching into my E-commerce API.

The goal was to understand how Redis can reduce repeated MongoDB queries by temporarily storing frequently requested product data.

## What I Learned

- Connected Redis to the E-commerce API using Docker
- Learned and practiced core Redis operations
- Implemented dynamic cache keys for product queries
- Implemented product caching with cache hit and cache miss handling
- Learned how Redis expiration works using TTL
- Learned how cached data can be stored and retrieved as JSON

## Redis Setup

Redis was run using Docker:

```bash
docker run -d --name redis-learning -p 6379:6379 redis
```

The Node.js application connects to Redis using the Redis client.

```text
Node.js Application
        ↓
   Redis Client
        ↓
   localhost:6379
        ↓
   Docker Redis
```

## Core Redis Operations

Practiced:

```text
SET      → Store data
GET      → Retrieve data
DEL      → Delete data
EXISTS   → Check if a key exists
EXPIRE   → Set expiration time
TTL      → Check remaining expiration time
```

## Product Caching

The product listing API now checks Redis before querying MongoDB.

```text
Client
  ↓
GET /products
  ↓
Create Cache Key
  ↓
Check Redis
  ↓
 ┌─────────────┐
 │ Cache Hit?  │
 └──────┬──────┘
    YES │       │ NO
        ↓       ↓
      Redis   MongoDB
        ↓       ↓
      Return  Save to Redis
                ↓
              Return
```

## Cache Keys

Because product results depend on different query parameters, a dynamic cache key is generated using:

```text
search
category
minPrice
maxPrice
page
limit
sort
```

This allows different product queries to have separate cache entries.

## Cache Expiration

Cached product results are stored with a 60-second expiration:

```js
await redisClient.set(cacheKey, JSON.stringify(result), {
  EX: 60,
});
```

This prevents cached data from remaining indefinitely.

## Testing

Tested the caching flow successfully:

```text
First request  → CACHE MISS
Second request → CACHE HIT
```

The first request fetched the data from MongoDB and stored it in Redis.

The second identical request returned the cached data from Redis.

## Day 52 Result

Successfully integrated Redis caching into the E-commerce API and verified the cache miss and cache hit workflow.

This gave me practical experience with using Redis as a caching layer alongside MongoDB.

**Day 52 — Complete.**
