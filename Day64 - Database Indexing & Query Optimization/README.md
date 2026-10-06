# Day 64 - Database Indexing & Query Optimization


## Overview

On Day 64, I learned how database indexes improve query performance and how to optimize database queries.

## What I Learned

- How database indexes speed up queries
- Single-field and compound indexes
- The leftmost-prefix rule for compound indexes
- `COLLSCAN` vs `IXSCAN`
- Using `explain()` to analyze query execution
- Trade-offs between faster reads, storage, and write performance

## Indexing

An index allows the database to find matching documents more efficiently instead of scanning the entire collection.

```text
Query
  ↓
Index
  ↓
Matching Document
```

## Compound Index

A compound index contains multiple fields:

```js
db.users.createIndex({
  country: 1,
  age: 1
})
```

The order of fields matters because of the leftmost-prefix rule.

## Query Analysis

MongoDB's `explain()` can show how a query is executed.

```js
db.users.find({
  email: "someone@gmail.com"
}).explain("executionStats")
```

Important stages include:

- `COLLSCAN` — collection scan
- `IXSCAN` — index scan

## Index Trade-offs

Indexes can make reads faster, but they also:

- Require additional storage
- Add overhead to writes
- Need to be maintained when indexed data changes

Therefore, indexes should be created for fields that are frequently queried, filtered, or sorted.

## Day 64 Result

I now understand how database indexes improve query performance, how compound indexes work, and how to use `explain()` to understand whether MongoDB is using an index effectively.
