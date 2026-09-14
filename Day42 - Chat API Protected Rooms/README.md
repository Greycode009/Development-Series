# Day 42 - Protected Rooms

## Project

Real-Time Chat API

Repository: https://github.com/Greycode009/Real-Time-Chat-API.git

## Overview

On Day 42, I added authorization to the real-time chat rooms.

The goal was to build on the JWT authentication from Day 41 and make sure that being authenticated does not automatically mean a user can access every room.

## What I Learned

- Difference between authentication and authorization
- How to authorize Socket.IO room access
- How to check user permissions before joining a room
- How the server should control room access
- How to send success and error events back to the client
- Why the client should not assume an action succeeded without server confirmation

## Implementation

The server checks the authenticated user's identity before allowing access to protected rooms.

The `admin` room is restricted to authorized users, while other rooms remain accessible to authenticated users.

The server also sends a response to the client after processing a room join request.

## Room Access Flow

Client requests room
↓
Server receives `room:join`
↓
Check authentication
↓
Check authorization
↓
Allowed → Join room → Send success
↓
Rejected → Send error

## Testing

Tested the following cases:

- Authorized user → `admin` room accepted
- Unauthorized user → `admin` room rejected
- Authenticated user → normal rooms accepted
- Client receives room join success from the server
- Client receives an error when room access is denied
- Existing messaging functionality continues to work

## Day 42 Result

Protected room access and server-side authorization are now implemented.

Next, the project will focus on real-time notifications.