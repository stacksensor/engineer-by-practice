# Exercise 004 - NATS: Lightweight, High-Speed Messaging

### Objective
Master the speed of light. Understand **NATS**—a cloud-native, high-performance messaging system designed for microservices and IoT. Learn why NATS is often preferred over Kafka/RabbitMQ for high-speed, "Fire-and-forget" communication, and understand the difference between **Core NATS** (Fast/Volatile) and **JetStream** (Stateful/Durable).

### Core Concepts to Master
- **Core NATS:** An extremely fast, memory-only pub/sub system. No persistence. If no one is listening, the message is lost.
- **JetStream:** The built-in persistence layer for NATS. Adds "At-least-once" and "Exactly-once" capabilities.
- **Subject-Based Messaging:** Using hierarchical strings (e.g., `orders.us.new`) instead of fixed topics.
- **Request-Reply Pattern:** A built-in NATS feature that simplifies synchronous-style calls over an asynchronous protocol.

### Research Topics
- "NATS vs RabbitMQ: Performance and Complexity"
- "What is JetStream and how does it compare to Kafka?"
- "The concept of 'Subject' in NATS"
- "Service Discovery using NATS"

---

### The Practical Challenge

**Part 1: The Zero-Footprint Speed**
1. Research the binary size and RAM usage of NATS vs Kafka. 
2. (Answer: NATS is ~20MB and uses tiny amounts of RAM; Kafka requires a JVM and GBs of RAM).
3. Discuss: Why does this make NATS the perfect choice for "Edge Computing" or "Raspberry Pi" projects?

**Part 2: The Request-Reply Pattern**
1. Service A sends a message on subject `get_price`. 
2. Service B hears it, calculates the price, and sends a message back to a "Hidden reply subject" that NATS created.
3. Discuss: How is this DIFFERENT from a standard HTTP call? (Answer: It’s automatically load-balanced across all instances of Service B by NATS).

**Part 3: Wildcard Filtering**
1. Subject hierarchy: `region.service.action`.
2. Subscriber 1 listens to `us.auth.*`.
3. Subscriber 2 listens to `*.#` (everything).
4. You send `us.auth.login`. Which subscribers hear it? (Answer: Both).
5. You send `eu.payment.success`. Which subscribers hear it? (Answer: Only 2).

**Part 4: Identifying the use case**
1. Use Core NATS for: (Answer: High-speed telemetry, heartbeats, logs you don't mind losing).
2. Use JetStream for: (Answer: Financial transactions, critical orders).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Data Loss. If you use Core NATS and your consumer app crashes for 1 second, you lose all messages sent during that second.
- **Gotcha 2:** Subject Overload. Because subjects are just strings, it is very easy to misspell one (`orders.new` vs `orders.mew`), resulting in messages being sent to a void with no errors reported.

### Reflection Question
Why is NATS considered the "Nerve System" for modern microservices? (Answer: Because it provides a single, high-speed way to do Pub/Sub, Work Queues, and Request-Reply).
