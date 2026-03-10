# Exercise 007 - Architecture Blueprinting

### Objective
Graduate to "System Architect." Apply all the components you've learned in Topic 015—Microservices, Caching, Queues, and Load Balancers—to design a comprehensive architectural blueprint for a massive, high-scale application (e.g., a Video Streaming Service or a Real-time Chat platform).

### Core Concepts to Master
- **System Design Diagrams:** Using tools like Excalidraw, Lucidchart, or Mermaid.js to visualize data flows and component boundaries.
- **Scaling Strategies:** Vertical Scaling (More RAM/CPU) vs Horizontal Scaling (More Servers).
- **Availability vs Consistency (CAP Theorem):** Understanding why you usually have to choose between "Always Available" and "Perfectly Consistent" in a distributed system.
- **Cost Estimation:** Estimating the cloud costs (AWS/Azure) for your proposed architecture.

### Research Topics
- "System Design Interview patterns"
- "Designing a YouTube clone architecture"
- "What is the CAP Theorem?"
- "High availability architecture best practices"

---

### The Practical Challenge

**Part 1: The High-Level Requirement**
1. Choose a complex scenario: "Design a Food Delivery System (like UberEats/DoorDash) that handles 1 million orders per day."
2. List the core services needed: `User Service`, `Restaurant Service`, `Driver Tracking`, `Orders`, and `Payments`.
3. Decide which service needs a "Message Queue" (e.g., matching drivers) and which needs a "Cache" (e.g., restaurant menus).

**Part 2: The Data Flow Diagram**
1. Using Excalidraw or a physical whiteboard, draw the "Happy Path" of an order.
2. User -> Load Balancer -> API Gateway -> Order Service -> DB.
3. Simultaneously: Order Service -> RabbitMQ -> Driver App.
4. Driver coordinates -> Redis (Real-time tracking).
5. Ensure there is no "Single Point of Failure" (e.g., if one database goes down, can the rest of the app still function?).

**Part 3: Scaling Audit**
1. What happens when it's Friday night and orders increase by 10x?
2. Implement "Horizontal Pod Autoscaling" (conceptual). Identify which services need more instances (the Gateway and Order service) and which need larger hardware (the Database).
3. Discuss "Database Sharding"—splitting the database by region (e.g., New York, London, Tokyo) to reduce load on a single cluster.

**Part 4: The Final Presentation**
1. Document your design in a `DESIGN.md` file.
2. Justify every architectural choice: "Why did you use Redis for tracking but SQL for orders?"
3. List the "Edge Cases": What happens if the Payment service is down? What happens if two drivers "accept" the same order at the exact same millisecond?
4. Congratulations. You have moved beyond "Coding" into the world of "Systems Engineering."

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-Engineering. Don't add a message queue for a "Contact Us" form on a blog. Only add complex architectural layers when they solve a specific problem (bottleneck, reliability, or scale).
- **Gotcha 2:** Ignoring Latency. Every box in your diagram represents a new network hop. If a user request must travel through 10 different microservices before responding, the UI will be painfully slow.

### Reflection Question
If a system is "99.99% Available," how many minutes of downtime are allowed per year? (Hint: Research 'The Nines of Availability'). drum
