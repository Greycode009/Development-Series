# Day 48 - Docker Compose

## Project

**Docker Learning**

## Overview

On Day 48, I continued learning Docker by focusing on Docker Compose.

The goal was to understand how multiple containers can be defined and managed together as a single application.

## What I Learned

- Learned the fundamentals of Docker Compose
- Created a `compose.yaml` file to define multiple services
- Ran a Node.js/Express API and MongoDB together
- Learned how Docker Compose networking works
- Understood communication between containers using service names
- Learned how `docker compose up` manages multiple services

## Docker Compose Configuration

The Compose setup defined two services:

```yaml
services:
  api:
    build: .
    ports:
      - "3000:3000"

  mongodb:
    image: mongo:8
```

The `api` service is built using the Dockerfile in the current directory, while the `mongodb` service uses the MongoDB image.

## Service Networking

Docker Compose creates a network for the services.

The API can communicate with MongoDB using the service name:

```text
mongodb
```

Instead of using:

```text
localhost
```

This is because `localhost` inside the API container refers to the API container itself.

## Running the Application

The complete application stack can be started with:

```bash
docker compose up
```

This starts the defined services together.

## Day 48 Result

Successfully learned the fundamentals of Docker Compose and how multiple containers can work together as one application.
