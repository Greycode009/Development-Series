# Day 57 — Practical Load Balancing

## Project

https://github.com/Greycode009/E-commerce-API

## What I Learned

Day 57 turned the scalability concepts from Day 56 into a practical implementation.

### Topics Covered

- Horizontal scaling with multiple API instances
- Running multiple Node.js API instances on different ports
- Load Balancer fundamentals
- Round-Robin request distribution
- Request forwarding using Node.js
- Testing Load Balancer behavior
- Understanding server failure and the need for health checks

## Practical Implementation

### API Instances

Ran the same E-commerce API as three separate instances:

```text
API 1 → :3001
API 2 → :3002
API 3 → :3003
```

### Load Balancer

Created a basic Load Balancer running on:

```text
Load Balancer → :3000
```

Architecture:

```text
                  Client
                     ↓
             Load Balancer :3000
                     ↓
          ┌──────────┼──────────┐
          ↓          ↓          ↓
       :3001      :3002      :3003
       API 1      API 2      API 3
```

## Round-Robin

Implemented Round-Robin routing:

```text
Request 1 → 3001
Request 2 → 3002
Request 3 → 3003
Request 4 → 3001
...
```

The Load Balancer forwards requests to the selected API instance.

## Failure Testing

Tested the behavior when one API instance was stopped.

```text
3001 → Healthy
3002 → Failed
3003 → Healthy
```

The basic Round-Robin Load Balancer still attempted to send a request to the failed server.

This demonstrated why production Load Balancers need **health checks** to detect unhealthy instances and remove them from the routing pool.

## Key System Design Lesson

```text
Multiple API Instances
        ↓
Load Balancer
        ↓
Distribute Traffic
        ↓
Health Checks
        ↓
Route Only to Healthy Servers
```

## Day 57 Complete

Applied horizontal scaling and Load Balancing concepts practically by running multiple API instances and building a basic Round-Robin Load Balancer.

Health-check implementation will be explored as a future improvement.
