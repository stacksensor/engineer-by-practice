# Exercise 002 - WebSockets & Full-Duplex Communication

### Objective
Enable real-time, two-way interaction. Master **WebSockets** to move away from "Polling" (where the client asks the server for updates) to "Push" (where the server sends data to the client as soon as it's ready). Learn how to manage long-lived connections and handle the challenges of scale and state.

### Core Concepts to Master
- **The Handshake:** How a WebSocket connection starts as an HTTP request and "Upgrades" to a persistent TCP connection.
- **Full-Duplex:** The ability for both client and server to send messages at the same time independently.
- **State management:** Unlike REST (Stateless), a WebSocket server must track which user is connected to which "Socket."
- **Heartbeats & Timeouts:** Keeping connections alive and detecting "Ghost" connections (where the user has closed their laptop but the socket is still open).

### Research Topics
- "The WebSocket protocol (RFC 6455)"
- "Scaling WebSockets with Redis Pub/Sub"
- "WebSockets vs Server-Sent Events (SSE)"

---

### The Practical Challenge

**Part 1: The Simple Chat Server**
1. Use a library like `ws` (Node.js) or `websockets` (Python).
2. Create a server that accepts connections.
3. When a message is received from one client, "Broadcast" it to every other connected client.

**Part 2: The Browser Client**
1. Write a minimal HTML/JS file that uses the native `new WebSocket()` API.
2. Allow the user to type a message and send it to the server.
3. Display incoming messages in a list on the screen.

**Part 3: Handling Disconnects**
1. Implement a "Heartbeat" (Ping/Pong) mechanism. 
2. The server sends a "Ping" every 30 seconds. If the client doesn't "Pong" back, the server closes the socket.
3. Observe how this prevents your server from running out of memory due to dead connections.

**Part 4: Real-time State (Conceptual)**
1. Discuss: If you have 1,000,000 connected users across 10 servers, how does a message from a user on Server A reach their friend on Server B?
2. Research **Redis Pub/Sub** as a "Backplane" for WebSockets.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Proxy Barriers. Some older corporate firewalls and proxies block WebSocket "Upgrades." Use `wss://` (Secure WebSockets over TLS) to bypass most packet inspectors.
- **Gotcha 2:** Memory Leaks. Every open socket consumes RAM. If you don't clean up your internal "Users List" when a socket closes, your server will eventually crash.

### Reflection Question
Why is a WebSocket better than "Long Polling" for a high-intensity application like a Live Stock Trading dashboard?
