# Day 49 - Docker Deep Dive

## Project

**Docker Learning**

Repository: https://github.com/Greycode009/Docker-Learning.git

Docker Hub Image:

```text
greycode29/nodejs
```

## Overview

On Day 49, I continued my Docker learning journey by going deeper into Docker fundamentals and practicing the complete workflow of building, running, tagging, and publishing Docker images.

I also published my Node.js Docker image to Docker Hub so it can be pulled and run on other machines.

## What I Learned

- Improved my understanding of Docker fundamentals and workflow
- Practiced building and running Docker images
- Learned how to tag images for Docker Hub
- Pushed my Docker image to Docker Hub successfully
- Learned how published images can be pulled and run on other machines

## Docker Workflow

```text
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
docker run
    ↓
docker tag
    ↓
Docker Hub
    ↓
docker push
    ↓
Published Image
```

## Build the Image

Build the Docker image from the project directory:

```bash
docker build -t docker-learning .
```

Check available images:

```bash
docker images
```

## Run the Container

Run the Node.js application:

```bash
docker run -p 3000:3000 docker-learning
```

Then open:

```text
http://localhost:3000
```

## Tag the Image

Tag the local image for Docker Hub:

```bash
docker tag docker-learning greycode29/nodejs:latest
```

## Login to Docker Hub

```bash
docker login
```

## Push the Image

Push the image to Docker Hub:

```bash
docker push greycode29/nodejs:latest
```

## Pull the Image

The published image can be pulled with:

```bash
docker pull greycode29/nodejs:latest
```

## Run the Published Image

After pulling the image:

```bash
docker run -p 3000:3000 greycode29/nodejs:latest
```

## Useful Commands

```bash
docker images
docker ps
docker ps -a
docker stop <container-id>
docker rm <container-id>
docker rmi <image-id>
```

## Day 49 Result

Successfully practiced the Docker image workflow and published my Node.js Docker image to Docker Hub.

This gave me a better understanding of how Docker images can be packaged, shared, pulled, and run across different environments.
