# Exercise 003 - Caching Strategies: How to Fill the Cache

### Objective
Update the value. Master the three most common **Caching Strategies**: **Cache-Aside** (Lazy), **Write-Through** (Consistent), and **Write-Back** (Fastest). Learn which to use for your next "Twitter-like" app (Massive Reads) vs your "E-commerce-like" app (Critical Consistency).

### Core Concepts to Master
- **Cache-Aside (Lazy Loading):** The app checks the cache. If it's not there, it reads from the DB and *then* saves it in the cache for next time. (Most common).
- **Write-Through:** Every time you write a new value, you write to the DB AND the Cache at the SAME time. (Always fresh, but slower writes).
- **Write-Back (Write-Behind):** You write only to the Cache. The cache later "Batches" the changes and writes them to the DB in the background. (Super fast, but if the cache crashes before the DB is updated, you LOSE data!).
- **Read-Through:** The app only talks to the Cache. The "Cache" handles talking to the DB itself. (Very clean, but requires a "Smart" cache).

### Research Topics
- "Cache-Aside vs Write-Through: A comparison"
- "When would I use Write-Back for high-performance logs?"
- "The concept of 'Stale' data in a lazy cache"
- "Using 'Look-aside' in a React/Frontend app"

---

### The Practical Challenge

**Part 1: The "Legacy" Migration (Scenario)**
1. You have a DB with 1,000,000 users. 
2. You want to add a cache.
3. If you use **Cache-Aside**, how does the cache "Fill up" for the first time? 
4. (Answer: One user at a time, whenever someone is looked up). 
5. Discuss why the first 1,000 users will experience "Cache Misses" (Slow), but the next 10,000 will be "Cache Hits" (Fast).

**Part 2: The "Consistent" Store**
1. Scenario: You are building a "Bank Balance" app. 
2. Use **Write-Through**. 
3. Discuss why this ensures that the "Cache" and the "DB" always have the same balance. 
4. If you used **Cache-Aside**, what happens if you update the DB balance to $500 but "Forgot" to update the Cache ($400)? (Answer: The user sees the old balance for 1 hour until the TTL expires!).

**Part 3: The "Log" Speedup**
1. You are receiving 1,000,000 "Game Event" logs per second. 
2. Discuss why **Write-Back** is the only way to save these without overwhelming the database. 
3. (Answer: The cache "groups" 10,000 logs into one single SQL "INSERT" every second).

**Part 4: Identifying the strategy**
1. Which strategy for:
   - "A social network 'Like' count" (Answer: Write-Back or Cache-Aside).
   - "A critical 'Reset Password' token" (Answer: Write-Through).
   - "A list of 'Trending' articles" (Answer: Cache-Aside).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Data Inconsistency. If your app crashes after the DB update but *before* the Cache update, your cache is now "Lying" to the user. Always use a **Transaction** or a "Delete Cache" rule.
- **Gotcha 2:** Cache Warming. If you reboot a server with a "New" cache, your DB might crash because every user is hitting the DB at once (The "Thundering Herd" problem). (Solution: "Warm up" the cache with the most popular data first).

### Reflection Question
Why is "Cache-Aside" the most popular strategy despite being "Inconsistent" compared to the others? (Answer: Because it works with any existing database and doesn't require complex "Distributed Transactions").
