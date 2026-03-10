# Exercise 003 - Edge Storage & KV Stores

### Objective
High-speed data at the fingertips. Master **Edge Key-Value (KV) Stores**. Learn how to store small amounts of data (like configuration, session tokens, or redirects) directly on the edge network for ultra-low latency access, and understand the trade-offs of **Eventual Consistency** in a global storage system.

### Core Concepts to Master
- **Edge KV:** A distributed, eventually consistent key-value store optimized for read-heavy workloads at the edge.
- **Write Latency:** Why writing to a KV store is slow (propagating to hundreds of regions) while reading is fast.
- **Eventual Consistency:** Accepting that when you update a key, a user in London might see the new value immediately while a user in Tokyo might see the old value for another 60 seconds.
- **Durable Objects:** (Advanced) A stateful edge storage model that provides "Strong Consistency" by pinning the state to a single geographic location.

### Research Topics
- "Cloudflare Workers KV vs Durable Objects"
- "When to use an Edge KV store?"
- "The CAP Theorem in edge storage systems"

---

### The Practical Challenge

**Part 1: The Redirect Engine**
1. Create a Cloudflare Workers project.
2. Initialize a KV namespace named `REDIRECTS`.
3. Fill the KV with keys like `short/github` -> `https://github.com/my-profile`.
4. Write a script that:
   - Takes a URL path (e.g., `/short/github`).
   - Looks it up in the KV store.
   - Redirects the user with a 301.

**Part 2: Managing Configuration**
1. Use KV to store an "Emergency Maintenance Mode" flag.
2. Update your worker to check this flag on every request. 
3. If the flag is `true`, show a "Down for maintenance" page.
4. Discuss: How fast can you flip this switch globally?

**Part 3: The Pricing Experiment**
1. Imagine an e-commerce site using KV to store product prices.
2. Discuss the risk of a "Sale" starting: If you update the price from $100 to $50, what happens if some users still see $100 for a few minutes due to eventual consistency?
3. How would you design a "Timestamp-based" price in KV to solve this?

**Part 4: Caching API Results**
1. Use a worker to fetch data from an expensive, slow API in a central region (e.g., AWS us-east-1).
2. Store the result in KV with an expiration time.
3. On the next request, serve the result from KV.
4. Measure the latency difference between the "Cold" call and the "Warm" KV call.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Global Write Limits. Many KV stores have limits on how many writes per second you can perform (e.g., 1 write per second per key). They are NOT for high-frequency updates.
- **Gotcha 2:** The "Replication Lag." Never use a standard Edge KV for something that requires "Strict Atomicity" (like decreasing a bank balance or a limited inventory count).

### Reflection Question
Why is a KV store a better choice for "User Login Sessions" than a traditional centralized Redis instance in a global application?
