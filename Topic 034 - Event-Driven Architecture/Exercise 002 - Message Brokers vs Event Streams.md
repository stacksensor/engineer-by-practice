# Exercise 002 - Message Brokers vs. Event Streams

### Objective
Pick the right pipe. Master the difference between **Traditional Message Brokers** (like RabbitMQ or NATS) and **Event Streaming Platforms** (like Kafka or Pulsar). Learn the difference between "Smart Broker / Dumb Consumer" and "Dumb Broker / Smart Consumer," and understand when you need a "Queue" vs a "Log."

### Core Concepts to Master
- **Message Broker (Queue):** Deletes the message once it is consumed. Great for tasks (e.g., "Resize this image").
- **Event Stream (Log):** Persists the messages indefinitely (or for a set time). Many consumers can read the same data at their own pace. Great for history and analytics.
- **Push vs. Pull:** Brokers "push" work to workers. Streaming clients "pull" data from the log.
- **The Offset:** In streaming, the client tracks "Where am I in the log?" (like a bookmark).

### Research Topics
- "RabbitMQ vs Kafka: The architectural difference"
- "Competing Consumers pattern in RabbitMQ"
- "Log-structured storage in Kafka"
- "What is NATS and why is it so fast?"

---

### The Practical Challenge

**Part 1: The "Delete on Read" Experiment**
1. Imagine a RabbitMQ queue with 10 messages. 
2. Consumer A reads all 10. 
3. Consumer B starts up. How many messages does it see? (Answer: 0).
4. Now imagine a Kafka Topic with 10 messages. 
5. Consumer A reads all 10.
6. Consumer B starts up. How many messages can it see? (Answer: All 10, by resetting its offset).

**Part 2: The "Competing Consumers" Test**
1. You have a queue of 1,000 "Orders to process." 
2. You spin up 5 workers. 
3. Discuss: How does a Message Broker ensure that two workers don't process the SAME order? (Answer: Locking/Acknowledgements).

**Part 3: The "Replay" Scenario**
1. Your "Analytics" code had a bug for the last 3 days. 
2. Discuss why Kafka makes it easy to fix the bug and "Replay" the last 3 days of data, while RabbitMQ makes this almost impossible unless you had a separate backup.

**Part 4: Identifying the use case**
1. Which would you use for:
   - "Sending a password reset email" (Answer: Broker/Queue).
   - "Tracking user clicks for a real-time recommendation engine" (Answer: Stream/Log).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Queue Depth. If your workers are slower than your producers in a Message Broker, the memory/disk usage can balloon until the broker crashes.
- **Gotcha 2:** Partitioning. In Streaming (Kafka), if you have 3 partitions, you can only have 3 concurrent consumers in a group. Adding a 4th consumer won't speed things up!

### Reflection Question
Why is a "Log-based" stream (Kafka) considered more "Immutable" and "Auditable" than a traditional "Queue" (RabbitMQ)? (Answer: Because the data stays after it's been read).
