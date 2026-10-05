# Day 63 - Database Replication

## Project

**Development Series**

Repository: https://github.com/Greycode009/Development-Series

## Overview

On Day 63, I learned about database replication and how it can be used to improve read scalability and availability.

The focus was on Primary and Read Replica architecture, replication lag, read-after-write consistency, and how replication works together with database sharding.

## What I Learned

- How database replication creates copies of data
- How Primary and Read Replica databases work
- How replicas can handle read-heavy workloads
- What replication lag means
- Why read-after-write consistency sometimes requires reading from the Primary
- The difference between sharding and replication
- How sharding and replication can be combined
- The difference between synchronous and asynchronous replication

## Primary and Read Replica

The Primary database generally handles write operations:

```text
INSERT
UPDATE
DELETE
```

Read Replicas can handle read operations:

```text
SELECT
```

The Primary continuously replicates changes to the replicas.

## Replication Flow

```text
Application
     |
     v
  Primary
     |
     | Replication
     v
+---------+---------+
|                   |
v                   v
Replica 1        Replica 2
   |                |
   +------ Reads ---+
```

## Replication Lag

Replication may not always happen instantly.

```text
Write
  |
  v
Primary
  |
  | small delay
  v
Replica
```

This delay is called **replication lag**.

Because of this, a read immediately after a write may need to go to the Primary when the latest data must be visible immediately.

## Sharding vs Replication

### Sharding

**Sharding = Split**

Sharding divides data across multiple databases or shards.

```text
Database
   |
   +--- Shard 1
   +--- Shard 2
   +--- Shard 3
```

### Replication

**Replication = Copy**

Replication creates copies of data.

```text
Primary
  |
  +--- Replica 1
  +--- Replica 2
```

### Using Both

Large systems can combine both approaches:

```text
Application
     |
Database Router
  /    |    \
 v     v     v
Shard 1 Shard 2 Shard 3
  |       |       |
Primary Primary Primary
 / \     / \     / \
R1  R2   R1  R2   R1  R2
```

Sharding distributes the dataset, while replication provides copies for read scaling and availability.

## Synchronous vs Asynchronous Replication

### Synchronous Replication

The Primary waits for confirmation from the replica before considering the operation complete.

```text
Write
  |
Primary
  |
Replica
  |
Confirmation
  |
Success
```

It provides stronger consistency but can make writes slower.

### Asynchronous Replication

The Primary can confirm the write without waiting for the replica.

```text
Write
  |
Primary -----> Success
  |
  +----------> Replica
```

It can provide faster writes but may introduce replication lag.

## Day 63 Result

I now understand how database replication works, how read replicas help scale read-heavy systems, and how replication can be combined with sharding to build scalable database architectures.
