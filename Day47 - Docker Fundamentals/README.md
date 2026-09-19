# Day 47 - Docker Fundamentals

## Project

**Docker Learning**

## Overview

On Day 47, I took a break from the Real-Time Chat API roadmap and focused on learning Docker fundamentals.

I learned how Docker packages applications into containers and practiced Docker with a small Node.js/Express application.

## What I Learned

- The relationship between Dockerfile, Docker Image, and Docker Container
- How to create a Dockerfile for a Node.js application
- How to build and run Docker images
- How Docker port mapping works
- How multiple containers can run from the same image
- How `.dockerignore` prevents unnecessary files from being included
- How Docker volumes provide persistent storage

## Docker Flow

```text
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
docker run
    ↓
Docker Container
```

## Implementation

Created a simple Node.js/Express application and Dockerized it using a Dockerfile.

The application was successfully built into a Docker image and run inside a container.

Port mapping was tested using:

```bash
docker run -p 3000:3000 docker-learning
```

Multiple containers were also run from the same image using different host ports.

## Docker Volumes

Created and tested a Docker volume to understand persistent storage.

The test demonstrated that data stored in a Docker volume remains available even after the container using it is removed.

## Key Concepts

### Dockerfile

Contains the instructions Docker follows to build an image.

### Image

A reusable blueprint containing the application and its required environment.

### Container

A running instance of a Docker image.

### Port Mapping

Maps a port on the host machine to a port inside the container.

### Volume

Provides persistent storage that can exist independently from a container.

## Day 47 Result

Successfully built and ran a Dockerized Node.js/Express application and learned the core concepts needed to continue with Docker Compose and multi-container applications.
