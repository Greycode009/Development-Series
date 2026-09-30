# Day 58 — Load Balancer Health Checks

## Project

https://github.com/Greycode009/E-commerce-API

## What I Learned

Day 58 focused on making the Load Balancer more reliable by detecting unavailable API instances before forwarding requests.

### Topics Covered

- Load Balancer health checks
- Detecting unavailable API instances
- Skipping unhealthy servers
- Healthy server routing
- Server failure and recovery testing

## Implementation

The Load Balancer now checks the health of API instances before routing requests:

```text
             Load Balancer
                   ↓
          Check Server Health
                   ↓
        ┌──────────┼──────────┐
        ↓          ↓          ↓
      3001       3002       3003
       OK          X          OK
        |                     |
        └──────────┬──────────┘
                   ↓
          Route to Healthy
             Instances
```

### Health Check Flow

```text
Request
   ↓
Check API Instance
   ↓
Healthy? ── Yes → Forward Request
   |
   No
   ↓
Skip Server
   ↓
Check Next Instance
```

## Failure Testing

Stopped one API instance and verified that the Load Balancer detected the unavailable server and continued routing requests through healthy instances.

## Key System Design Lesson

Health checks prevent a Load Balancer from sending traffic to unavailable servers, improving system reliability and fault tolerance.

## Day 58 Complete

Implemented and tested health-aware routing for the Load Balancer.
