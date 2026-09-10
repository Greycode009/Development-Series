# Day 38 - Room-Based Messaging

**GitHub Repository:** [Real-Time Chat API](https://github.com/Greycode009/Real-Time-Chat-API.git)

## Today's Progress

* Refactored Socket.IO into a **feature-based structure**
* Implemented **room join & leave** functionality
* Added **room-based message broadcasting**
* Tested **real-time communication between separate rooms**

## Architecture

Refactored the Socket.IO event handling into feature-based modules:

```text
src/
├── features/
│   ├── chat/
│   │   └── chat.socket.js
│   └── room/
│       └── room.socket.js
└── app.js
```

This keeps chat and room-specific socket logic separated from the main application setup.

## Room-Based Messaging

Implemented Socket.IO rooms to allow users to communicate within specific rooms.

```text
Client
   ↓
room:join
   ↓
Server
   ↓
socket.join(room)
   ↓
Room
```

Messages are now broadcast only to users inside the selected room:

```js
io.to(room).emit("message:receive", message);
```

## Room Management

Added support for:

* Joining a room
* Leaving a room
* Sending messages to a specific room
* Testing communication between separate rooms

## Day 38 Outcome

Moved the project toward a cleaner **feature-based architecture** and implemented the foundation for isolated real-time conversations using Socket.IO rooms.

**Next:** Continue building the chat system with message persistence.
