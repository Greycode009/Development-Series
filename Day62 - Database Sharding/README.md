# Day 62 — Database Sharding

## Overview

Day 62 focused on database sharding and how large-scale systems distribute data and database workload across multiple databases.

## What I Learned

- Database sharding fundamentals
- Shard keys and data distribution
- Uneven sharding and database hotspots
- Sharding vs read replicas
- Combining sharding with read replicas

## Database Sharding

When a database becomes very large and handles a heavy workload, storing all the data in one database can become difficult to scale.

Sharding divides the data across multiple databases.

```text
              Application
                   ↓
              Sharded DB
             /    |    \
          Shard1 Shard2 Shard3
```

Each shard stores a portion of the overall data.

## Shard Key

A shard key is the value used to determine which shard should store or serve a particular piece of data.

For example, `userId` can be used as a shard key.

```text
User ID
   ↓
Shard Key
   ↓
Determine the correct shard
```

For a request such as:

```text
GET /users/12345
```

the system can use the `userId` to determine which shard contains the user's data instead of searching every database.

## Uneven Sharding and Hotspots

A poor shard key can cause uneven data distribution.

For example:

```text
0–20   → Shard 1
21–40  → Shard 2
41–60  → Shard 3
```

If most users fall into the `21–40` range, Shard 2 may receive much more data and traffic than the other shards.

This creates a **hotspot**.

A good shard key should distribute data and workload as evenly as possible.

## Sharding vs Read Replicas

### Sharding

Sharding distributes **data and database workload** across multiple databases.

```text
Data
 ↓
Shard 1
Shard 2
Shard 3
```

### Read Replicas

Read replicas distribute **read traffic** across multiple database instances.

```text
Primary DB
   ↓
Replicas
```

The key difference is:

```text
Sharding     → Distributes data/workload
Read Replica → Distributes read traffic
```

## Sharding + Read Replicas

Both techniques can be combined in a large-scale system.

```text
             Application
                  ↓
              Sharded DB
             /    |    \
          Shard1 Shard2 Shard3
           ↓       ↓       ↓
        Replicas Replicas Replicas
```

Sharding distributes the data and database workload, while replicas help distribute read traffic within the database architecture.

## Key Lesson

Database scaling is not only about adding more API servers.

As systems grow, the database can become a major bottleneck. Sharding helps distribute data and workload across multiple databases, while read replicas help distribute read traffic.

Understanding when and how to use these techniques is an important part of designing scalable systems.

## Day 62 Complete

Learned the fundamentals of database sharding, shard keys, data distribution, hotspots, and the difference between sharding and read replicas.
