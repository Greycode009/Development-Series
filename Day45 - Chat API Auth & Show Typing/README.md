# Day 45 - Independent Real-Time Challenge

## Project

**Real-Time Chat API**

Repository: https://github.com/Greycode009/Real-Time-Chat-API.git

## Overview

On Day 45, I expanded the Real-Time Chat API with a basic user authentication system and a real-time typing indicator.

The authentication system allows users to register and log in without manually creating JWT tokens. The typing indicator allows users to see when another user is typing in the same room.

## What I Learned

- How to implement basic user registration and login
- How to securely hash passwords using Argon2
- How to generate JWTs after successful login
- How to connect the client to Socket.IO using an authenticated JWT
- How to implement real-time typing indicators with Socket.IO
- How authenticated users can interact with real-time features

## Authentication Flow

```text
Register
   ↓
User stored with hashed password
   ↓
Login
   ↓
Password verification
   ↓
JWT generated
   ↓
Client stores JWT
   ↓
Socket.IO connection authenticated