# Exercise 004 - Cache Invalidation: The Hardest Problem

### Objective
Kill the old data. Master **Cache Invalidation**—the act of deleting "Old" (Stale) data from the cache so the "New" data can take its place. Learn why Phil Karlton famously said "There are only two hard things in Computer Science: cache invalidation and naming things." Understand the difference between **Time-To-Live (TTL)** and **Event-Driven Invalidation**.

### Core Concepts to Master
- **TTL (Time To Live):** A "Countdown" timer (e.g., 5 minutes) after which the cache deletes itself automatically. (Simple, but data stays "Stale" for 5 minutes).
- **Explicit Invalidation:** Your code says `cache.delete("user:123")` whenever the user's name changes. (Fastest, but easy to forget to do it).
- **Event-Driven Invalidation:** A separate service watches the database and tells the cache when to update. (Most robust, but complex to build).
- **Stale-while-revalidate:** Showing the "Old" data while fetching the "New" data in the background. (Best for user experience).

### Research Topics
- "Why is cache invalidation hard?"
- "The pros and cons of TTL (Time-To-Live)"
- "Using Pub/Sub (Redis) for cache invalidation"
- "Implementation of 'Stale-while-revalidate' in Vercel/SWR or React Query"

---

### The Practical Challenge

**Part 1: The "Old Name" Problem (TTL)**
1. You cache a user's name: `Alex`. TTL = 10 minutes. 
2. Alex changes their name to `Alexander` in the DB at 12:00:01.
3. At 12:05:00, Alex visits their profile. 
4. Which name do they see? (Answer: `Alex`).
5. Discuss: Will Alex be confused? 
6. (Answer: Yes, "Why didn't my name change?!").

**Part 2: The "Immediate" Fix (Explicit)**
1. In your `updateName()` function, add one line: `delete_cache("user:123")`. 
2. Discuss why this fixes the problem instantly. 
3. But... what if you have **10 different functions** that update a user (e.g., `updateProfile`, `updateAvatar`, `updateEmail`) and you forget to add the "Delete cache" line to the new `updateBio` function? 
4. (Answer: You are back to "Stale" data!).

**Part 3: The "Automatic" Messenger (Event-Driven)**
1. Research how **Kafka** or **Postgres Triggers** can be used to send a "User updated" message to every server. 
2. Discuss why this ensures the cache is deleted on every machine, even if your API code is messy.

**Part 4: Identifying the strategy**
1. Which strategy for:
   - "A 'News' site with 10,000 articles" (Answer: TTL or SWR).
   - "A 'Stock Price' that changes once a second" (Answer: Event-Driven or very low TTL).
   - "A 'Terms of Service' page" (Answer: Long TTL - maybe 24 hours).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The Invalidation Storm. If you delete "All users" from the cache at once, every single user will hit the database at the SAME time, crashing the server.
- **Gotcha 2:** The "Version" mismatch. If you update the Cache but the DB update fails, your Cache is now "Lying" about the future. (Solution: Delete the cache *after* the DB update is finished).

### Reflection Question
Why is "Time-To-Live" (TTL) the #1 choice for most developers, despite its "Staleness" problem? (Answer: Because it is the only strategy that is "Bulletproof" - even if your code is buggy, the cache will eventually clean itself).
