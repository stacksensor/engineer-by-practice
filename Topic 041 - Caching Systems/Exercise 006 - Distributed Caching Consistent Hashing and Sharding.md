# Exercise 006 - Distributed Caching: Consistent Hashing

### Objective
Scale the RAM. Master **Distributed Caching**—the art of using 10 separate servers to act like one "Giant" 1TB cache. Learn why simple **Modulo Hashing** (`key % 10`) is a disaster for caching and understand how **Consistent Hashing** allows you to add or remove servers without losing all your data.

### Core Concepts to Master
- **Sharding:** Splitting a 10TB cache into 10 servers of 1TB each.
- **The Hash Function:** Turning a string ("User_123") into a number (1,000,000).
- **Modulo Hashing:** `Hash(key) % Server_Count`. (Simple, but if Server_Count changes, EVERY key maps to the wrong server).
- **Consistent Hashing:** Arranging servers and keys on a "Circle" (the Hash Ring). Each key is assigned to the next server "Clockwise."
- **Data Loss on Scale:** Why "Resizing" the cache shouldn't cause a total outage.

### Research Topics
- "How Consistent Hashing works: A visual guide"
- "Adding and removing nodes in a distributed cache"
- "The Modulo Problem: Why adding a server is slow"
- "The concept of 'Virtual Nodes' in Consistent Hashing"

---

### The Practical Challenge

**Part 1: The "Modulo" Disaster (Math)**
1. You have 3 Cache Servers (0, 1, 2).
2. Key "User_123" maps to CPU hash 100.
3. `100 % 3 = 1` (Server 1).
4. You add a 4th server (0, 1, 2, 3).
5. `100 % 4 = 0` (Server 0).
6. Discuss: If every key in your cache just "Moved" to a new server, what is your **Cache Hit Rate**?
7. (Answer: Near 0%! You have to re-read everything from the database, which might crash the DB).

**Part 2: The Consistent Hash Ring**
1. Imagine a circle from 0 to 1,000,000. 
2. Server A is at 100,000. Server B is at 500,000. Server C is at 900,000.
3. User_123 is at 150,000. 
4. User_123 goes to the "Next" server on the ring. (Answer: Server B).
5. If you add **Server D** at 700,000, which users move? 
6. (Answer: Only the ones between 500k and 700k. All others stay where they are!).
7. Discuss: Why does this only affect a tiny % of the cache instead of 100%?

**Part 3: The "Wait" state**
1. Research how **Redis Cluster** handles this using "Hash Slots" (16,384 slots). 
2. Is it the same as Consistent Hashing? (Answer: Close! It’s a fixed-size ring where ranges are moved).

**Part 4: Identifying the sharding**
1. Research the **`redis-cli`** command to see which "Node" a key belongs to. 
2. (Hint: `CLUSTER KEYSLOT <key>`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Uneven Distribution. If you are unlucky, 90% of your keys might end up on Server A while Server B is empty. (Solution: Use "Virtual Nodes" - place the same server in 100 different spots on the ring).
- **Gotcha 2:** The "Hot" Key. If "User_1" is a celebrity with 1,000,000 followers, one single server will be overwhelmed while the others are idle. (Solution: Duplicate "Hot" keys to all servers).

### Reflection Question
Why is Consistent Hashing the core technology behind almost every "Global" internet scale system (like Amazon DynamoDB, Cassandra, and Akamai CDN)? (Answer: Because it is the only way to scale "Elasticly" without causing a massive outage every time you resize).
