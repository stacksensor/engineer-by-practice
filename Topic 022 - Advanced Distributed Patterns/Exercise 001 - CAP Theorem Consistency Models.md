# Exercise 001 - CAP Theorem & Consistency Models

### Objective
Understand the fundamental limits of distributed systems. Explore the **CAP Theorem** (Consistency, Availability, Partition Tolerance) and learn why you must always choose between Consistency and Availability during a network failure, and explore modern consistency models like "Eventual Consistency" vs "Strong Consistency."

### Core Concepts to Master
- **Consistency (C):** Every read receives the most recent write or an error.
- **Availability (A):** Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
- **Partition Tolerance (P):** The system continues to operate despite an arbitrary number of messages being dropped by the network between nodes.
- **PACELC Theorem:** An extension of CAP that describes the trade-off between Latency and Consistency even when there is *no* network failure.
- **Eventual Consistency:** A guarantee that if no new updates are made to an object, eventually all accesses will return the last updated value (e.g., DNS, Amazon DynamoDB).

### Research Topics
- "The CAP Theorem simplified"
- "Strong vs Eventual Consistency examples"
- "What is the PACELC theorem?"
- "Linearizability vs Serializability"

---

### The Practical Challenge

**Part 1: The Partition Simulation**
1. Imagine a distributed database with 2 nodes (A and B).
2. A user writes `value = 10` to Node A. 
3. The network between A and B breaks (A Partition).
4. Another user tries to read `value` from Node B.
5. Discuss: 
   - If Node B returns `value = null` (stale data), it has chosen **Availability** over Consistency.
   - If Node B returns an `Error` (waiting for the sync), it has chosen **Consistency** over Availability.

**Part 2: Real-world Mapping**
1. Identify 3 databases and categorize them:
   - **CP (Consistency/Partition):** e.g., MongoDB (default), Redis, HBase.
   - **AP (Availability/Partition):** e.g., Cassandra, CouchDB, DynamoDB.
   - **CA (Consistency/Availability):** Explain why CA is technically impossible in a network-distributed system.

**Part 3: Testing Consistency**
1. Research the "Read-Your-Writes" consistency model.
2. If you update your profile on a website and immediately refresh the page, but see the old data, which consistency model is the site likely using?
3. How would you solve this on the frontend to improve user experience?

**Part 4: The PACELC Trade-off**
1. Research the "L" (Latency) in PACELC.
2. Even when the network is healthy, why does forcing "Strong Consistency" (waiting for all nodes to acknowledge a write) increase the latency for the user?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "P" is not optional. In the real world, networks *will* fail. You cannot choose "CA." You are always building a "CP" or "AP" system.
- **Gotcha 2:** Defaults Matter. Many databases (like MongoDB) can be configured to be EITHER CP or AP depending on how you set your "Write Concern" and "Read Preference."

### Reflection Question
Why are most "Banking Systems" designed as CP (Consistency) while most "Social Media Feeds" are designed as AP (Availability)?
