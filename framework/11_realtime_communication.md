[← Back to Index](./README.md)

# 11. Real-time & Bidirectional Communication

The web isn't just request/response anymore. Sometimes the server needs to talk to the client.

## Junior -> Mid: The Basics
**Goal:** Can build a simple chat app or notification system.

### 1. Polling (The Old Way)
- **Concept:** Asking "Are we there yet?"
- **Key Skills:**
    - **Short Polling:** Client requests `/messages` every 5 seconds. Simple but inefficient.

### 2. WebSockets
- **Concept:** A persistent 2-way pipe.
- **Key Skills:**
    - **Handshake:** Upgrading HTTP to WebSocket.
    - **Events:** `socket.on('message')` and `socket.emit('message')`.
    - **Broadcasting:** Sending a message to all connected clients.

---

## Mid -> Senior: Protocols & Patterns
**Goal:** Chooses the right tool for the job and handles connection state.

### 1. Server-Sent Events (SSE)
- **Concept:** One-way radio (Server -> Client).
- **Key Knowledge:**
    - **Use Case:** Stock tickers, news feeds, progress bars.
    - **Pros/Cons:** Simpler than WebSockets (standard HTTP), but text-only and one-way.

### 2. Channels & Rooms
- **Concept:** Organizing traffic.
- **Key Knowledge:**
    - **Pub/Sub:** Subscribing a user to "Room 123".
    - **Private Channels:** Authenticating that a user is allowed to listen to a channel.

### 3. State Management
- **Concept:** Who is online?
- **Key Knowledge:**
    - **Presence:** Tracking online/offline status.
    - **Reconnection:** Handling network drops and automatically rejoining channels.

---

## Senior -> Lead: Scale & Infrastructure
**Goal:** Scales real-time apps beyond a single server.

### 1. Scaling WebSockets
- **Concept:** The "Socket ID" problem.
- **Key Knowledge:**
    - **Sticky Sessions:** Ensuring a client stays connected to the same server.
    - **Redis Adapter / Backplane:** If User A is on Server 1 and User B is on Server 2, how do they chat? You need a Pub/Sub layer (Redis) to bridge the servers.

### 2. Protocol Details
- **Concept:** Optimizing the wire.
- **Key Knowledge:**
    - **Heartbeats / Pings:** Detecting dead connections (zombie sockets) and closing them to save resources.
    - **Binary Protocols:** Using MQTT or raw binary data for IoT/Gaming to reduce latency.

### 3. Serverless Real-time
- **Concept:** Not managing connections.
- **Key Knowledge:**
    - **Managed Services:** AWS AppSync, Pusher, Firebase. Offloading the connection management so your backend remains stateless.
