# Day 41 - JWT Socket Authentication

## Project

Real-Time Chat API

Repository: https://github.com/Greycode009/Real-Time-Chat-API.git

## Overview

On Day 41, I replaced the temporary username-based Socket.IO authentication with proper JWT-based authentication.

The goal was to authenticate users during the Socket.IO connection handshake and allow the server to control the user's identity.

## What I Learned

- How JWT authentication works with Socket.IO
- How to send authentication data through the Socket.IO handshake
- How to verify JWTs on the server
- How Socket.IO middleware can protect socket connections
- How to extract user information from a verified JWT
- How to attach authenticated user information to a socket
- Why the server should control message sender identity instead of trusting the client
- How to reject connections with missing or invalid authentication

## Implementation

The client sends a JWT when establishing the Socket.IO connection.

The server uses Socket.IO middleware to:

1. Receive the JWT from the handshake
2. Verify the token using the JWT secret
3. Extract the authenticated user's information
4. Attach the user information to the socket
5. Reject the connection if authentication fails

The authenticated identity is then used when handling chat messages.

## Authentication Flow

Client
↓
Socket.IO handshake
↓
JWT authentication middleware
↓
JWT verification
↓
Authenticated user attached to socket
↓
Socket connection accepted
↓
Messages use authenticated sender identity

## Testing

Tested the following cases:

- Valid JWT → connection accepted
- Invalid JWT → connection rejected
- Missing JWT → connection rejected
- Authenticated user identity available on the socket
- Existing room functionality continues to work
- Messages use the authenticated sender identity

## Day 41 Result

JWT-based Socket.IO authentication is now implemented and working.

Next, the project will move toward protecting chat rooms using the authenticated socket identity.