# Exercise 002 - In-Memory Caching: Redis vs. Memcached

### Objective
Store it in RAM. Master the two most popular tools for **In-Memory Caching**: **Redis** and **Memcached**. Learn why storing data in the server's RAM is 100x faster than reading from a database and understand which tool to choose for a "Simple Key-Value" vs a "Complex Data Structure" app.

### Core Concepts to Master
- **Memory-only:** Everything is stored in the server's RAM. If the server crashes, all data is (usually) lost.
- **Memcached:** Simple, multi-threaded, very fast "Key-Value" store. (The "Old school" reliable choice).
- **Redis (REmote DIctionary Server):** "Smart" cache that supports lists, sets, hashes, and "Persistence" (saving to disk optionally).
- **Single-threaded (Redis):** Every command in Redis must finish before the next one starts. (Ensures consistency).
- **Key-Value Store:** How to store "User_123" -> `{"name": "Alex"}`.

### Research Topics
- "Redis vs Memcached: A side-by-side comparison"
- "Why the RAM is faster than the SSD"
- "Redis Data Types: Strings, Hashes, Lists, Sets"
- "The concept of 'Key Eviction' (what happens when the RAM is full?)"

---

### The Practical Challenge

**Part 1: The Speed Test (Conceptual)**
1. **DB (Postgres):** 5ms to find a user.
2. **Redis:** 0.2ms to find a user.
3. If you have 10,000 users per second, calculate the "Total Time" spent waiting for the DB vs Redis. 
4. (Answer: DB = 50,000ms total; Redis = 2,000ms total. Redis saves 48 seconds of CPU time *every second*).

**Part 2: The Data Choice**
1. Scenario A: "You just need to store 1,000,000 HTML fragments strings for 1 hour." (Answer: Memcached).
2. Scenario B: "You want a 'Real-time Leaderboard' of 100 players that always stays sorted." (Answer: Redis - use 'Sorted Sets').
3. Scenario C: "You want a 'Job Queue' where you can push and pop items." (Answer: Redis - use 'Lists').

**Part 3: The Single-Thread Paradox**
1. Research why **Redis** is single-threaded but still faster than almost any multi-threaded database. 
2. (Answer: No "locks" or context switching overhead, and everything is in RAM).

**Part 4: Identifying the "Key" design**
1. How should you name your keys? 
2. Research the standard format: `object:id:field` (e.g., `user:101:profile`). 
3. Discuss why using a "Colon" makes searching and grouping keys easier.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Filling the RAM. If you don't set a **TTL** (Time To Live), your cache will grow until it takes up 100% of the server RAM, crashing the OS.
- **Gotcha 2:** The "Reboot" surprise. If you use the cache as a "Primary Database" and the power goes out, all your data is gone forever. Caches are for "Transient" data, not "Permanent" data (unless you enable Redis Persistence).

### Reflection Question
Why is the "Key-Value" model so much faster than the "Relational" model (SQL) for simple lookups? (Answer: No 'JOINs,' no complex 'WHERE' parsing; it's a direct dictionary jump).
