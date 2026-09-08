# Day 36 - WebSocket Foundations

## Project 5 - Real-Time Chat API

**GitHub Repository:** [Real-Time Chat API](https://github.com/Greycode009/Real-Time-Chat-API.git)

### Today's Progress

* Learned the fundamentals of **WebSockets** and real-time communication
* Understood the difference between **REST APIs and WebSockets**
* Learned the **WebSocket connection lifecycle**
* Understood **events and bidirectional communication**
* Explored the basic **real-time messaging flow** between clients and server

### Key Concepts Learned

#### REST API

REST follows a **request → response** communication model:

```text
Client → Request → Server
Client ← Response ← Server
```

The client must initiate communication.

#### WebSocket

WebSockets maintain a persistent connection that allows **both the client and server to communicate in real time**:

```text
Client ←────────→ Server
       Connection
```

Either side can send events while the connection remains open.

### WebSocket Connection Lifecycle

```text
Connect
   ↓
Communicate
   ↓
Send / Receive Events
   ↓
Disconnect
```

### REST vs WebSocket

| REST                      | WebSocket                      |
| ------------------------- | ------------------------------ |
| Request/Response          | Real-time communication        |
| Client initiates requests | Both sides can communicate     |
| Short-lived requests      | Persistent connection          |
| Uses routes/endpoints     | Uses events                    |
| Good for CRUD APIs        | Good for chat and live updates |

### Day 36 Outcome

Built a strong conceptual foundation for **WebSocket-based backend development** and understood how real-time communication differs from the REST APIs built in the previous E-commerce API project.

**Next:** Create the Real-Time Chat API project and establish the first WebSocket connection.
