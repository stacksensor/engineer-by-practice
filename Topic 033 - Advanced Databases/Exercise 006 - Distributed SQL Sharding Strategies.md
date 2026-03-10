# Exercise 006 - Distributed SQL & Sharding Strategies

### Objective
Scale the unscalable. Master the concepts of **Distributed SQL** and **Sharding**. Learn how to split a single massive database across multiple physical servers when it becomes too large for one machine, and understand the complexities of **Cross-shard Queries** and **Global Secondary Indexes**.

### Core Concepts to Master
- **Vertical Scaling:** Buying a bigger server (limited).
- **Horizontal Scaling / Sharding:** Splitting data across many small servers (unlimited scale).
- **Shard Key:** The column used to decide which server a row belongs to (e.g., `user_id % 10`).
- **Distributed Joins:** The extreme difficulty of joining two tables that live on different physical servers.
- **Replication Factor:** Storing the same shard on 3 servers for high availability.

### Research Topics
- "What is Database Sharding?"
- "Choosing the right Shard Key"
- "Distributed SQL databases: CockroachDB, TiDB, YugabyteDB"
- "The drawbacks of sharding"

---

### The Practical Challenge

**Part 1: The Shard Key Audit**
1. Imagine an app with 1,000,000,000 users.
2. Discuss the pros/cons of these Shard Keys:
   - `country_id`: (Pro: Data stays in region. Con: China/US shards will be 100x bigger than Iceland shard).
   - `user_id` (Random UUID): (Pro: Perfectly balanced. Con: You can't query "all users in Germany" without hitting every single server).

**Part 2: The Hot Spot Problem**
1. You shard by `created_at` timestamp. 
2. Discuss why this is a terrible idea for a fast-growing app. (Answer: All "New" data goes to the newest shard, while the old shards sit idle. You've created a "Hot Spot").

**Part 3: Distributed SQL (Conceptual)**
1. Research **CockroachDB**. 
2. Explain how it provides a "Single Database" appearance to the developer while actually running across 10-100 nodes. 
3. How does it handle a "Leader" failure? (Hint: **Raft consensus**).

**Part 4: The Joins Nightmare**
1. You have `Orders` sharded by `order_id` and `Products` sharded by `product_id`.
2. Discuss why a query joining these two is 1,000x slower than on a single-server database.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Sharding too early. Most apps never reach the size where sharding is required. Sharding adds massive complexity to your code and your operations team.
- **Gotcha 2:** Fixed Shards. If you hardcode "10 shards" in your logic, it's very painful to increase it to 20 shards later (you have to move every single row!). Use **Consistent Hashing** or a distributed SQL engine to handle this.

### Reflection Question
Why is "Distributed SQL" considered the "Holy Grail" of database engineering compared to traditional manual sharding? (Answer: It provides ACID and SQL features while scaling automatically).
