# Exercise 007 - State Management in Streaming Systems

### Objective
Remember the past. Master **State Management** in streaming systems. Learn how a system that is "Always running" survives if it crashes and needs to remember a total it has been calculating for 3 months. Understand the difference between **Local State** (Fast) and **Checkpointing** (Reliable).

### Core Concepts to Master
- **Stateful Operators:** Operations like `window`, `join`, and `aggregate` that require memory.
- **RocksDB:** The high-speed embedded database used by Kafka Streams and Flink to store state on the local disk.
- **Checkpointing / Savepoints:** Periodically backing up the local state to a "Long-term" store (like S3) so it can be recovered if the server dies.
- **Change Log Topic:** In Kafka Streams, every update to the "State" is also written back to a Kafka topic as a "Backup log."
- **Sidecar Queries:** Querying the "Internal State" of a streaming app directly from a web UI (e.g., "Tell me the Current Total for user 5" without looking at a separate database).

### Research Topics
- "How Flink manages state (Checkpoints vs Savepoints)"
- "RocksDB as a state backend"
- "Interactive Queries in Kafka Streams"
- "Scaling a stateful streaming application"

---

### The Practical Challenge

**Part 1: The Recovery Simulation**
1. You are summing up "Total Revenue" for the year. The current total is $5,000,000.
2. The server crashes and its RAM is wiped.
3. Discuss the 2 recovery paths:
   - **Path A (No Checkpoint):** You have to re-read every single purchase since Jan 1st. (Slow!).
   - **Path B (With Checkpoint):** You load the snapshot from 2:00 PM and only re-read the last 5 minutes of data. (Fast!).

**Part 2: The RocksDB local disk**
1. Research why we store state on the **Local Disk** (RocksDB) rather than in an external database (like Postgres).
2. (Answer: Network latency! Reading from Postgres for every single event would make the stream 1,000x slower).

**Part 3: Interactive Queries (Concept)**
1. Research how to expose the "State" of a Kafka Streams app as a REST API.
2. Discuss why this is exciting: Your streaming app *is* the database. You don't need a separate SQL server to show "Current Balance" to the user.

**Part 4: Scaling Out**
1. You have 10GB of state on 1 server. You want to scale to 2 servers.
2. Discuss: How does the engine "Move" 5GB of state (RocksDB files) to the new server? (Hint: Sharding state by Key).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** State "Bloat." If you store a list of every product a user has looked at, and your app runs for 5 years, your state will eventually be larger than your disk capacity. Use **State TTL** (Time To Live) to expire old data.
- **Gotcha 2:** Checkpoint Pressure. Running a checkpoint every 1 second can consume 50% of your disk bandwidth, slowing down the actual processing of messages.

### Reflection Question
Why is the "Internal State" of a streaming engine often considered more "Accurate" than a downstream SQL database? (Answer: Because the streaming engine handles the exact offsets and guarantees required for correctness).
