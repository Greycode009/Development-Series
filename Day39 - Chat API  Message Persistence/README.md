# Day 39 - Message Persistence & Presence

**GitHub Repository:** https://github.com/Greycode009/Real-Time-Chat-API.git

## Today's Progress

- Added **MongoDB message persistence** using Mongoose
- Implemented **message history** when users join a room
- Added a **chat service** for retrieving stored messages
- Implemented **online/offline presence tracking**
- Added **room-based presence updates**

## Message Persistence

Previously, messages only existed during the active Socket.IO connection.

Now messages are stored in MongoDB:

```text
Client
   ↓
message:send
   ↓
Validate
   ↓
MongoDB
   ↓
Broadcast