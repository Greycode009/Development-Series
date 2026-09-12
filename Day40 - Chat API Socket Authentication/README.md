# Day 40 - Socket Authentication

**GitHub Repository:** https://github.com/Greycode009/Real-Time-Chat-API.git

## Today's Progress

- Added **Socket.IO handshake authentication**
- Attached the authenticated username to the socket
- Used the server-side socket identity for messages
- Added sender information to persisted messages

## Socket Authentication

The client now sends authentication data when establishing the Socket.IO connection:

```js
const socket = io("http://localhost:3000", {
  auth: {
    username: "Dipesh",
  },
});