# Day 37 - Real-Time Messaging & Chat Rooms

**GitHub Repository:** [Real-Time Chat API](https://github.com/Greycode009/Real-Time-Chat-API)

## Today's Progress

* Implemented real-time messaging with **Socket.IO**
* Built **client-to-server and server-to-client** communication
* Added **message broadcasting** to multiple clients
* Added **structured message payloads** and basic validation
* Implemented **disconnect handling**
* Implemented **chat room joining**

## Key Concepts Learned

### Socket.IO Events

Learned how `emit()` and `on()` work:

```text
emit() → Send an event
on()   → Listen for an event
```

### Message Flow

```text
Client
   ↓ message:send
Server
   ↓ message:receive
Connected Clients
```

### Broadcasting

Implemented broadcasting using:

```js
io.emit("message:receive", message);
```

This sends the event to all connected clients.

### Structured Messages

Messages are now sent as objects:

```json
{
  "text": "Hello bro!"
}
```

This provides a foundation for adding more message information later.

### Message Validation

Added basic server-side validation to prevent invalid message payloads from being broadcast.

### Chat Rooms

Implemented room joining using:

```js
socket.join("developers");
```

Clients can now join a specific Socket.IO room.

## Day 37 Outcome

Built the core foundation for real-time chat communication using **Socket.IO**, including events, broadcasting, structured messages, validation, disconnect handling, and room joining.

**Next:** Implement room-based message broadcasting so messages are delivered only to users inside the selected chat room.
