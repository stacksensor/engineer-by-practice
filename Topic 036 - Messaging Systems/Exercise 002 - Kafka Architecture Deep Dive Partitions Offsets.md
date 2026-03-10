# Exercise 002 - Kafka Architecture (Partitions & Offsets)

### Objective
Master the engine of scale. Understand the internal anatomy of **Apache Kafka**. Learn how **Partitions** allow a single topic to be spread across multiple servers, how **Offsets** track consumer progress, and how **Consumer Groups** enable effortless horizontal scaling.

### Core Concepts to Master
- **The Topic:** A logical category (e.g., "orders").
- **The Partition:** The unit of parallelism. A topic is split into multiple partitions, and each is an append-only log.
- **The Offset:** A unique integer assigned to every message in a partition. It is the "Address" of the message.
- **Consumer Group:** A group of workers that share the load of one topic. Each worker is assigned a set of partitions.
- **Broker:** A single Kafka server. A "Cluster" is a collection of brokers.

### Research Topics
- "How Kafka Partitions work"
- "Zookeeper vs KRaft in modern Kafka"
- "Rebalancing in a Consumer Group"
- "Compacted Topics: Keeping only the latest value"

---

### The Practical Challenge

**Part 1: The Parallelism Limit**
1. You have a topic with **3 partitions**.
2. You spin up a Consumer Group with **5 workers**.
3. Discuss: How many workers are "Active" and how many are "Idle"? 
4. (Answer: 3 active, 2 idle. A partition can only be read by ONE worker in a group at a time).

**Part 2: The "Order" Guarantee**
1. Discuss: Kafka guarantees the order of messages *inside a partition*, but NOT *across the whole topic*.
2. If you have 3 partitions, and messages happen in this order: `A(1), B(2), C(3), D(4)`.
3. If `A` and `C` go to Partition 1, and `B` and `D` go to Partition 2. 
4. Can `B` be processed before `A`? (Answer: Yes, because they are on different servers).
5. Discuss how to fix this using a **Key**. (Answer: If you send all messages for User 1 to the same partition, User 1's events stay perfectly ordered).

**Part 3: The Offset Reset**
1. A consumer crashes and restarts 5 minutes later.
2. How does it know where to start? (Answer: It looks at the **__consumer_offsets** internal topic to find its last "Bookmark").
3. Discuss the difference between `auto.offset.reset = earliest` vs `latest`.

**Part 4: Identifying the Broker Role**
1. Research the **Controller** broker. What happens if it dies? (Answer: A new Controller is elected automatically).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Partition count is hard to change. If you start with 2 partitions and want 10 later, your "Key-to-Partition" mapping will change, breaking your ordering guarantees.
- **Gotcha 2:** The "Rebalance Storm." If you have 100 consumers and one dies, Kafka pauses ALL 100 while it recalculates who gets which partition. This can cause a massive spike in latency.

### Reflection Question
Why did Kafka choose to make the "Consumer" responsible for tracking progress (Offsets) rather than the "Broker"? (Answer: To allow the broker to be "Dumb" and extremely fast).
