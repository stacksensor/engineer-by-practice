# Exercise 004 - Real-Time State (Durable Objects)

### Objective
Maintain state on the move. Master **Durable Objects**, a revolutionary pattern for building stateful edge applications. Learn how to ensure **Strong Consistency** by routing all traffic for a specific "ID" (like a chat room or a document) to a single instance running in a specific data center, enabling real-time collaboration at the edge.

### Core Concepts to Master
- **Durable Object:** A class-based instance in Cloudflare Workers that has local storage and a unique, persistent identity.
- **Strong Consistency:** Guarantees that every read for a specific object sees the latest write, no matter which gateway the user entered through.
- **Coordination:** Using a Durable Object as a "Middelman" for WebSockets to allow multiple users to see the same state at the same time.
- **Waking up vs Hibernating:** How the platform automatically creates the object when needed and shuts it down to save money when it's idle.

### Research Topics
- "What are Cloudflare Durable Objects?"
- "Building a collaborative real-time editor with Durable Objects"
- "Strong Consistency vs Eventual Consistency in edge state"

---

### The Practical Challenge

**Part 1: The Counter Object**
1. Research the syntax for a Durable Object class.
2. Define an `increment()` method that stores a value in the object's local `storage`.
3. Create a Worker that:
   - Takes a "counter name" in the URL.
   - Gets a handle to the Durable Object for that name.
   - Calls `increment()` and returns the total.
4. Test with multiple users hitting the same counter name. Verify that the count is always accurate and consistent.

**Part 2: The Chat Room (Conceptual)**
1. Design a real-time chat room using a Durable Object.
2. The Durable Object acts as the "Server" for a group of WebSockets. 
3. When a user sends a message, the Durable Object receives it and sends it out to all other connected users.
4. Discuss: If Room A is in NYC and Room B is in London, where will the Durable Objects for each room physically run?

**Part 3: Handling Concurrency**
1. Research the `alarm()` API for Durable Objects. 
2. Explain how an object can "Schedule" a task for the future even if no users are currently connected (e.g., "Clean up inactive chat logs in 24 hours").

**Part 4: The Geo-Routing**
1. Discuss the "Speed of Light" trade-off: Durable Objects are "Strongly Consistent" because they live in one place.
2. If a user in India connects to a chat room created by a user in NYC, will their latency be higher or lower than a standard "Edge KV" lookup? Why?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Local Storage Limits. Durable Objects can usually store about 10GB of data. They are for "Active State," not for building a full data warehouse.
- **Gotcha 2:** The "Singleton" Performance. Because all traffic for a specific ID goes to a single instance, if you have 1,000,000 users all trying to talk to the *same* Durable Object at once, it will become a bottleneck.

### Reflection Question
How does a Durable Object combine the "Easy Scaling" of serverless with the "Global Consistency" of a traditional SQL database?
