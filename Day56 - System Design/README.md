# Day 56 — System Design & Scalability

## Project

https://github.com/Greycode009/E-commerce-API

## What I Learned

Day 56 marked the start of the System Design track alongside backend development.

### Topics Covered

- Scalability fundamentals
- Vertical vs horizontal scaling
- Stateful vs stateless architecture
- Why stateless APIs are important for horizontal scaling
- Identifying system bottlenecks
- Basic scalable architecture for the E-commerce API

## Architecture

### Current Simple Architecture

```text
Client
  ↓
Node.js / Express API
  ↓
MongoDB
```

### Scalable Architecture Concept

```text
              Users
                ↓
          Load Balancer
                ↓
      ┌─────────┼─────────┐
      ↓         ↓         ↓
    API 1     API 2     API 3
      └─────────┼─────────┘
                ↓
              Redis
                ↓
             MongoDB
```

## Key System Design Mindset

```text
Requirement
    ↓
Identify Bottleneck
    ↓
Choose Solution
    ↓
Understand Trade-offs
```

## Day 56 Complete

Started applying system design thinking to the existing E-commerce API and learned the foundations required for building scalable systems.
