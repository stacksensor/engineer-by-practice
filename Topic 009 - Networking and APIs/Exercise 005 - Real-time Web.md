# Exercise 005 - Real-time Web (WebSockets & SSE)

### Objective
Transition from request-response models into persistent server-client architectures. Master the underlying streaming tech that powers real-time multiplayer applications and push notification frameworks.

### Core Concepts to Master
- **WebSockets:** The persistent bi-directional communication protocol natively supported in modern browsers.
- **Server-Sent Events (SSE):** A unidirectional HTTP channel designed purely for the server to push updates down to the client automatically.
- **Long Polling:** The legacy hack where browsers hold HTTP requests open intentionally until the server responds, simulating a real-time connection.
- **The Upgrade Header:** How standard HTTP seamlessly escalates into a raw TCP stream automatically.

### Research Topics
- "WebSockets vs Server-Sent Events differences"
- "Socket.io basics and rooms"
- "Implementing native EventSource in JavaScript"

---

### The Practical Challenge

**Part 1: The Socket Connection**
1. Connect to an echo socket terminal: `let ws = new WebSocket("wss://echo.websocket.org/");`
2. Initialize specific callbacks automatically attached to the persistent instance natively.
3. Write `ws.onopen = () => console.log("Connected");`
4. Send a test message immediately when the connection resolves: `ws.send("Trigger Event");`

**Part 2: Bidirectional Parsing**
1. Attach an `onmessage` listener explicitly.
2. `ws.onmessage = (event) => console.log(event.data);`
3. Send JSON strings mapping complex payloads. Send `{"action":"jump", "player":1}` perfectly over the raw line.
4. You must parse the incoming string data precisely before injecting it into your application logic seamlessly.

**Part 3: One-Way Streaming (SSE)**
1. WebSockets are bidirectional. Sometimes you only need the server to send updates natively (like a stock ticker).
2. Instantiate `new EventSource("http://localhost/ticker");`
3. Map `.onmessage` identical to standard sockets.
4. The SSE connection operates permanently strictly over Layer 7 standard HTTP without upgrading, removing immense firewall security complexities typically seen with WSS configurations locally.

**Part 4: Handling Connection Drops**
1. Live network streams are inherently unstable natively across mobile cell towers securely.
2. Implement `.onclose` natively. When the event fires unexpectedly, log an error exactly.
3. Construct a standard `setTimeout` fallback recursively attempting to re-establish the `new WebSocket` identically after 3000 milliseconds mathematically.
4. This auto-reconnect logic validates client stability across varied networking zones automatically.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Attempting to send JavaScript objects directly into `ws.send()`. The underlying socket only transmits textual string streams or raw binary data bytes directly. Always invoke `JSON.stringify()` when deploying complex objects, and `JSON.parse()` the incoming `event.data` correctly.
- **Gotcha 2:** Security firewalls heavily aggressively block internal corporate traffic running on non-standard WS ports (like 8080). Production WebSocket servers historically must operate on port `443` identically mapping the standard encrypted HTTPS route cleanly.

### Reflection Question
What is the structural impact on RAM and server hardware if you deploy a standard Express server to actively manage 100,000 persistent socket connections instantly holding open variables versus spinning up stateless containers?