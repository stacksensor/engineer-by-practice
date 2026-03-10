# Exercise 005 - Cache Eviction: LRU vs. LFU

### Objective
Clean house. Master **Cache Eviction Policies**—the logic that tells the cache "Which item should I delete to make room for a new one?" Learn the two primary algorithms: **LRU (Least Recently Used)** and **LFU (Least Frequently Used)**. Understand how to "Optimize" which data stays in RAM and which one is "Kicked out."

### Core Concepts to Master
- **The Eviction Cache:** A cache with a "Max Size" (e.g., 100MB).
- **LRU (Least Recently Used):** Deletes the item that hasn't been "touched" for the longest time. (Most common).
- **LFU (Least Frequently Used):** Deletes the item that has been "touched" the fewest total times. (Best for "Trending" data).
- **FIFO (First-In, First-Out):** Deletes the "Oldest" item, regardless of how often it's used. (Simplest, but usually the worst performance).
- **Random Eviction:** Deletes a random item. (Better than you think!).

### Research Topics
- "How LRU (Least Recently Used) works (The 'Linked List' + 'Hash Map' trick)"
- "LRU vs LFU: Which should I pick for my cache?"
- "The concept of 'Approximated LRU' in Redis"
- "What is 'Thrashing' in a cache?"

---

### The Practical Challenge

**Part 1: The LRU Simulation**
1. Cache Capacity: 3 items.
2. Current State: `[User A (1m ago), User B (10s ago), User C (1s ago)]`.
3. You need to add **User D**. 
4. Which one is "Evicted"? (Answer: User A - the oldest "Touch").
5. Discuss: If User A is active at 1:02 PM, and then you add User D, does User A stay? (Answer: Yes, because its "Touch" time was just updated).

**Part 2: The LFU Difference**
1. Cache Capacity: 2 items.
2. Item 1: `Logo.png` (Used 1,000 times).
3. Item 2: `User_Profile` (Used 2 times, but was just updated 1 second ago).
4. You need to add **Item 3**.
5. If you use **LRU**, which one is deleted? (Answer: Logo.png - it hasn't been used in a while).
6. If you use **LFU**, which one is deleted? (Answer: User_Profile - it only has 2 uses total).
7. Discuss why LFU is better for "The Google Logo" or "The home page CSS" which everyone needs.

**Part 3: The "Wait" state**
1. Research how **Redis** implements LRU. 
2. (Answer: Instead of a perfect linked list, it picks 5 random items and deletes the 'Least recently used' one among them. This is much faster for a high-speed database).

**Part 4: Identifying the "Thrashing"**
1. Imagine a cache of 10 items. 
2. A user loops through 1,000 items in a "Scan." 
3. Discuss why the cache is now "Empty" (all useful data was evicted) and how to prevent a "Cache Scan" from killing your performance.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Tiny Cache. If your cache is too small (e.g., only 1,000 items for 10,000 active users), your "Hit Rate" will be zero because items are being evicted before they can even be used!
- **Gotcha 2:** Memory overhead. Every algorithm (like LFU) requires a "Counter" or a "Timestamp" for every single item. If you have 10,000,000 items, and each "Counter" takes 8 bytes, you just used 80MB of RAM just for the *counting*!

### Reflection Question
Why is LRU almost always the "Default" choice for caching systems like Redis, Memcached, and Operating Systems? (Answer: Because it is a great "Guesser" of what you will need next based on what you used most recently).
