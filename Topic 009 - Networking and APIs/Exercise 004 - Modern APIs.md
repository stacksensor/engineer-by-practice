# Exercise 004 - Modern APIs (GraphQL/WebSockets)

### Objective
Expand your architecture beyond standard REST configurations. Interface with GraphQL endpoints to selectively query exact data graphs, and construct WebSocket pipelines to hold two-way bidirectional open connections.

### Core Concepts to Master
- **GraphQL:** A query language allowing clients to dictate exactly what JSON keys the server returns.
- **Over-fetching vs Under-fetching:** Solving the REST problem where endpoints return too much data, or require multiple sequential queries to assemble a view.
- **WebSockets (ws://):** A persistent Layer-7 protocol that remains open, enabling instantaneous push notifications and two-way real-time communication.

### Research Topics
- "GraphQL queries and mutations tutorial"
- "REST vs GraphQL pros and cons"
- "How do WebSockets work in JavaScript"

---

### The Practical Challenge

**Part 1: The GraphQL Query**
1. Connect to the public Rick and Morty GraphQL API: `https://rickandmortyapi.com/graphql`.
2. Do not use standard `fetch` GET routes. 
3. Send a `POST` request to the endpoint. The body must contain your raw GraphQL string exactly:
   ```graphql
   query {
     character(id: "1") {
       name
       status
       species
     }
   }
   ```
4. Check the response. The server returns exactly those three keys, ignoring the other properties in the database.

**Part 2: Deep Graph Nesting**
1. Update your query.
2. Request the character's name and their `origin` location.
3. Inside the `origin` location, query the nested `dimension` string.
4. Note that while REST would require two separate API calls, GraphQL resolves this deep lookup in a single request.

**Part 3: The Persistent WebSocket**
1. Initialize a new WebSocket connection: `new WebSocket('wss://ws.postman-echo.com/raw')`.
2. Unlike HTTP, you must bind event listeners to the connection. Add an `onopen` handler.
3. Add an `onmessage` handler to log incoming payloads to the console.
4. Use `ws.send("Hello Server")` to push a string. The Postman echo server should reflect it back to you instantly.

**Part 4: Real-time UI Updates**
1. Build a simple HTML interface with an input box and a button.
2. Link the button click to send the input value over the WebSocket.
3. When `onmessage` triggers, display the received data in a UI list. You have now built a basic real-time echo interface.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** GraphQL queries are sent as `POST` requests, even for read operations. Ensure your `Content-Type` is set to `application/json` and your query is properly escaped in the request body.
- **Gotcha 2:** Memory Leaks. WebSockets maintain an active connection. If you are using React, you must call `ws.close()` in your cleanup function (e.g., when the component unmounts) to prevent resource leakage.

### Reflection Question
What are the primary performance and architectural advantages of using WebSockets instead of "Standard HTTP Polling" for a real-time multiplayer application?