# Day 51 - GitHub Actions Deployment

## Project

**GitHub Actions Learning**

## Overview

On Day 51, I moved from learning GitHub Actions concepts to implementing a real deployment workflow.

The goal was to understand how GitHub Actions can automatically connect to a remote server and deploy the latest version of an application.

## What I Learned

- Implemented a GitHub Actions deployment workflow
- Learned how to trigger workflows on `push` events
- Configured SSH-based server deployment
- Learned how Docker Compose can automate application deployment

## Deployment Workflow

```text
Developer
    ↓
git push
    ↓
GitHub Repository
    ↓
GitHub Actions
    ↓
Ubuntu Runner
    ↓
SSH Connection
    ↓
Remote Server
    ↓
git pull
    ↓
docker compose up -d --build
    ↓
Application Deployed