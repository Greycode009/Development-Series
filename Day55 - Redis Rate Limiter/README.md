# Day 55 — Redis API Rate Limiting

## Project

https://github.com/Greycode009/E-commerce-API

## What I Built

Implemented Redis-based API rate limiting in the E-commerce API.

### Features

- Tracks requests using Redis
- Limits product API requests to 10 requests per 60 seconds
- Returns HTTP 429 when the limit is exceeded
- Automatically resets the limit after the Redis key expires

## What I Learned

- How Redis can be used for request tracking
- How `INCR` maintains request counts
- How Redis expiration creates a time-based request window
- How rate limiting protects APIs from excessive requests

## Testing

- Verified requests 1–10 succeed
- Verified request 11 returns `429 Too Many Requests`
- Verified the request limit resets after 60 seconds

## Technologies

- Node.js
- Express.js
- Redis
- Docker
- MongoDB

## Day 55 Complete

Successfully implemented and tested Redis-based API rate limiting.
