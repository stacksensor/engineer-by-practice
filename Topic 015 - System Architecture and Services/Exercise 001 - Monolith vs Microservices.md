# Exercise 001 - Monolith vs Microservices

### Objective
Understand the evolution of backend architecture. Learn the conceptual and practical differences between a "Monolithic" server (a single large codebase) and "Microservices" (multiple independent, specialized services), and evaluate the trade-offs of each approach for scaling engineering teams.

### Core Concepts to Master
- **The Monolith:** A single application where all business logic (Auth, Payments, User Mgmt) lives in one repository and database.
- **Service Decomposition:** Breaking a monolith into smaller, focused services that communicate over a network (e.g., via HTTP or gRPC).
- **Loose Coupling:** Ensuring that a change or failure in one service (e.g., the Email service) does not crash the entire application.
- **Service Discovery:** How services find the network address (IP/Port) of other services at runtime.

### Research Topics
- "Microservices vs Monolith trade-offs"
- "Bounded Contexts in Domain-Driven Design (DDD)"
- "Challenges of Microservice networking (latency, consistency)"
- "What is a 12-factor app?"

---

### The Practical Challenge

**Part 1: The Monolith Skeleton**
1. Create a single Express application that handles two separate features: `Products` and `Reviews`.
2. Both features should share the same database and the same running process.
3. Observe how easy it is to perform a `JOIN` between Products and Reviews in your SQL queries. This is the primary advantage of a Monolith.

**Part 2: The Service Split**
1. Create a second, independent Express application.
2. Move the `Reviews` logic and database into this new server.
3. Now, if the `Products` server needs to see reviews, it cannot use a local SQL JOIN. It must perform a network request to the `Reviews` server.
4. Implement a `fetch` in the Products server to get review data from `http://localhost:3001/reviews`.

**Part 3: Handling Network Failure**
1. Intentionally stop your `Reviews` server.
2. Attempt to load a product page on your `Products` server.
3. Observe how the page might crash or hang. This is a "Cascading Failure."
4. Implement a "Circuit Breaker" or a simple timeout. If the reviews aren't available, show the product anyway and display an error message for the reviews section. This is "Graceful Degradation."

**Part 4: Data Consistency Challenges**
1. In a Monolith, deleting a product automatically deletes its reviews (Cascading Delete).
2. In Microservices, the `Reviews` database has no idea the product was deleted.
3. Discuss "Eventual Consistency." How can you notify the Reviews service to clean up its data when a product is removed from the other service? (Hint: Topic for Exercise 002).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Distributed Monolith." If your 10 microservices are so tightly connected that you must deploy them all at the exact same time, you have built a "Distributed Monolith," which has the disadvantages of both systems and the advantages of neither.
- **Gotcha 2:** Network Latency. In a monolith, a function call takes nanoseconds. In microservices, every "function call" is a network request that can take 10-100ms. Overusing microservices for small tasks will destroy your application's speed.

### Reflection Question
If your startup only has two developers, why is building a Microservice architecture almost always a bad business decision?
