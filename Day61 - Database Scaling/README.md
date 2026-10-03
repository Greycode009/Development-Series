# Day 61 — Database Scaling

## Overview

Day 61 introduced the fundamentals of database scaling and how databases can become bottlenecks when application traffic increases.

## What I Learned

- Database scaling fundamentals
- Database bottlenecks
- Primary database vs read replicas
- Read scaling
- Database replication
- Write → Primary
- Read → Replicas

## Database Bottleneck

When multiple API instances handle increasing traffic, they may still depend on the same database.

```text
          Load Balancer
          /     |     \
        API1  API2   API3
          \     |     /
           MongoDB
```

As traffic increases, a large number of requests can reach the database, making the database a potential bottleneck.

## Read Replicas

Read replicas can distribute read traffic across multiple database instances.

```text
             Primary DB
             ↑       ↓
          Writes   Replication
                    ↓
              ┌─────┴─────┐
              ↓           ↓
          Replica 1    Replica 2
              ↑           ↑
             Reads      Reads
```

The basic model is:

```text
Write → Primary
Read  → Replicas
```

## Replication

When data is written to the primary database, the changes are replicated to the read replicas.

This allows replicas to serve read requests while the primary handles writes.

## Key Lesson

Database scaling is important because scaling API servers alone does not remove the database bottleneck.

Read replicas help distribute read traffic and allow the system to handle a larger read workload.

## Day 61 Complete

Learned the foundation of database scaling, primary databases, read replicas, read scaling, and replication.
