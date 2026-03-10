# Exercise 005 - Real-time Pipelines (Kafka Streams / Flink)

### Objective
Connect the dots. Master the tools used to build **Real-time Pipelines**. Learn how to use **Kafka Streams** (A library for lightweight apps) and **Apache Flink** (A massive distributed engine) to Filter, Map, Join, and Aggregate data in motion. Understand how to build a pipeline that transforms "Raw Clicks" into "Active User Count" in milliseconds.

### Core Concepts to Master
- **Topology:** The "Map" of your pipeline (Source -> Transformation -> Sink).
- **KStream vs KTable:** In Kafka Streams, a "Stream" is every event since the start of time; a "Table" is the current state of every key.
- **State Store:** The internal database (usually RocksDB) that the engine uses to remember things (like "Total Sales so far today").
- **Backpressure:** The mechanism that tells the Producer to "Slow down" when the streaming engine is overwhelmed.

### Research Topics
- "Kafka Streams vs Apache Flink: When to use which?"
- "Building a stateless vs stateful pipeline"
- "Joining two streams in real-time"
- "What is a 'Sink' in a streaming pipeline?"

---

### The Practical Challenge

**Part 1: The Transformation Map**
1. Source: `{"user": 1, "action": "click", "price": 10}`.
2. Step 1: **Filter** (Remove any prices < 5).
3. Step 2: **Map** (Extract only the `price`).
4. Step 3: **Aggregate** (Sum of prices).
5. Sink: Write the total to a new Kafka topic.
6. Discuss: How many of these steps are "Stateless" (don't need memory) and which are "Stateful" (must remember the previous total)?

**Part 2: KStream vs KTable Battle**
1. You have a topic `user_locations`.
2. **Stream view:** `Alex at A`, `Alex at B`. (Result: You see his journey).
3. **Table view:** `Alex at B`. (Result: You only see where he is NOW).
4. Discuss: Which view would you use for "Calculating distance traveled" vs "Finding a driver near me"?

**Part 3: The Distributed Join**
1. Research how Flink joins two streams (e.g., `Purchases` and `Product_Details`).
2. Discuss why both streams must be "Co-partitioned" (sent to the same server) for the join to work fast.

**Part 4: Identifying the tool for the job**
1. Which tool for:
   - "A small Microservice that calculates tax on every order" (Answer: Kafka Streams).
   - "A massive system that analyzes 1 million sensor readings per second across a cluster of 50 servers" (Answer: Apache Flink).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Serialization overhead. Converting JSON to Objects and back to JSON for every step in the pipeline can consume 50% of your CPU. Use **Protobuf** or **Avro** for high-speed pipelines.
- **Gotcha 2:** The "Fat" State Store. If you try to join two topics with 1 Billion keys each, your streaming engine will run out of disk space for its local state store (RocksDB).

### Reflection Question
Why is a streaming pipeline considered "Inverting the Database"? (Hint: In a DB, data is passive and queries are active. In a stream, queries are passive and data is active).
