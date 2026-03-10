# Exercise 007 - Scaling Search Systems

### Objective
Graduate to search at scale. Learn how to manage high-availability and extreme performance in search engines by mastering **Sharding** (horizontal scaling of data) and **Replication** (horizontal scaling of queries), and understand the trade-offs between "Search Speed" and "Indexing Speed."

### Core Concepts to Master
- **Sharding:** Splitting a large index into smaller pieces (shards) that can be distributed across different servers.
- **Primary vs. Replica Shards:**
  - **Primary:** Where the "Write" happens.
  - **Replica:** A copy of the primary used for "Reads" and failover.
- **Cross-Cluster Replication (CCR):** Synchronizing an index between different geographical locations (e.g., US-East and EU-West).
- **Segments & Merging:** How Elasticsearch stores data on disk (Lucene segments) and why "Force Merging" can improve read performance.

### Research Topics
- "How many shards should an Elasticsearch index have?"
- "Scaling Pinecone with Pod types and replicas"
- "Elasticsearch index life cycle management (ILM)"

---

### The Practical Challenge

**Part 1: The Multi-Node Cluster**
1. Update your Docker Compose to run an Elasticsearch cluster with 3 nodes (`es01`, `es02`, `es03`).
2. Verify the health of the cluster: `GET /_cluster/health`. You should see `number_of_nodes: 3`.

**Part 2: Configuring Shards**
1. Create a new index `high-volume-logs` with `number_of_shards: 3` and `number_of_replicas: 1`.
2. Check the shard distribution: `GET /_cat/shards?v`. 
3. Observe how K8s/Elasticsearch has spread the shards across all 3 nodes.

**Part 3: The Failover Test**
1. Manually stop one of your Docker nodes (`docker stop es01`).
2. Run `GET /_cluster/health` again. Observe the status change from `green` to `yellow`.
3. Check the shards again. Note that the cluster has automatically promoted a "Replica" shard to be the new "Primary" for the missing data.
4. Restart the node and watch the cluster turn `green` again.

**Part 4: Index Lifecycle Management (ILM)**
1. Research the "Hot-Warm-Cold" architecture.
2. Explain how you would store "Today's logs" on fast SSD nodes (Hot) but move "3-month-old logs" to cheap HDD nodes (Cold) while keeping them searchable.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-sharding. Having too many tiny shards (e.g., 50 shards for 1GB of data) creates massive overhead and slows down the cluster. A good rule of thumb is keeping shard sizes between 10GB and 50GB.
- **Gotcha 2:** The "Split Brain" Problem. In a multi-node cluster, if nodes lose contact with each other, they might both try to become the "Master." Ensure you have a correctly configured `discovery.seed_hosts`.

### Reflection Question
Why do you add more **Replica** shards to a search engine when your website's traffic (number of users searching) increases, but not necessarily when your data (number of documents indexed) increases?
