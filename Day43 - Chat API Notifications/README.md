# Day 43 - Real-Time Notifications

## Project

Real-Time Chat API

Repository: https://github.com/Greycode009/Real-Time-Chat-API.git

## Overview

On Day 43, I added a basic real-time notification system to the chat application.

Notifications are delivered through Socket.IO when relevant events occur, while keeping notification handling separate from normal message delivery.

## What I Learned

- How real-time notifications work with Socket.IO
- How to create a dedicated notification feature
- How to emit events to other users in a room
- How to separate notifications from chat messages
- How the client listens for notification events
- How unread notification state can be represented in the UI

## Implementation

When a user sends a message, the server:

1. Saves the message
2. Delivers the message through `message:receive`
3. Sends a `notification:new` event to other users in the room

The notification contains information such as the sender, room, and message text.

## Notification Flow

User sends message
↓
Server saves message
↓
message:receive
↓
notification:new
↓
Other users receive notification
↓
Notification UI updates

## Testing

Tested the following:

- Real-time notification delivery
- Notifications received by other users
- Sender does not receive their own notification
- Notification unread count updates
- Notification information is displayed in the UI
- Existing chat functionality continues to work

## Day 43 Result

Basic real-time notifications are now implemented and connected to the chat system.