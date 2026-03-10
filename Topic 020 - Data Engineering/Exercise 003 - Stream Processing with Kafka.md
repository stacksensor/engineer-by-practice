# Exercise 003 - Stream Processing with Kafka

### Objective
Master "Real-time" data. Transition from "Batch Processing" (once an hour/day) to "Stream Processing" (millisecond latency). Learn how to use **Apache Kafka** as a distributed log to decouple producers (who send data) from consumers (who process data).

### Core Concepts to Master
- **The Event Log:** Kafka is not a queue; it's a persistent, distributed append-only log of "What happened."
- **Topics & Partitions:** How Kafka organizes data and parallelizes processing.
- **Producers & Consumers:** Applications that write to and read from Kafka.
- **Consumer Groups:** Scaling out data processing so that multiple consumers can share the workload of a single topic.
- **Retention Policy:** Defining how long data stays in Kafka (e.g., 7 days) before being deleted.

### Research Topics
- "What is Apache Kafka and why is it used?"
- "Kafka vs RabbitMQ: Key differences"
- "Understanding Kafka partitions and replication factor"

---

### The Practical Challenge

**Part 1: The Local Broker**
1. Run Kafka locally using Docker Compose (or use a managed service like Confluent Cloud).
2. Verify it is running by listing topics: `kafka-topics.sh --list`.

**Part 2: Producing Events**
1. Create a topic named `user-clicks`.
2. Write a Python script (using `confluent-kafka` or `kafka-python`) to send simulated click events (JSON) to the topic.
3. Every click should have a `user_id`, `url`, and `timestamp`.

**Part 3: Consuming Events**
1. Write a separate Consumer script that reads from the `user-clicks` topic.
2. Every time an event arrives, print: "User X clicked on URL Y at Z."
3. Run multiple instances of the consumer with the same `group.id`. Observe how the events are divided between the consumers.

**Part 4: Dealing with Failure**
1. Kill one of your consumer instances.
2. Watch as Kafka "Rebalances" and moves the traffic to the remaining healthy consumer.
3. Discuss the concept of "At-Least-Once" delivery. What happens if a consumer processes a message but crashes before telling Kafka "I'm done" (Acknowledge)?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Zookeeper Dependency. Most older versions of Kafka require a separate tool called Zookeeper to coordinate. Newer versions ("KRaft") are removing this, but it's still common to see both running.
- **Gotcha 2:** Serialization. If your producer sends data encoded in UTF-16 but your consumer expects UTF-8, you will get garbage data. Always agree on a standard (like JSON or Avro) before starting.

### Reflection Question
Why is Kafka considered a "Buffer" or "Shock Absorber" for systems where the Producer sends data much faster than the Consumer can process it?
