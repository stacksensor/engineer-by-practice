# Exercise 001 - The Hierarchy of Caching

### Objective
Respect the speed of light. Master the **Hierarchy of Caching**—the fundamental layers of memory from the CPU to the Internet. Learn the "Latencies" of different storage types and understand why a "Cache" is required to prevent the super-fast CPU from waiting for the super-slow Disk or Network.

### Core Concepts to Master
- **L1 / L2 Cache:** Extremely fast (nanoseconds) memory built directly into the CPU chip.
- **RAM (Memory):** Fast (10-100 nanoseconds) but volatile. This is where "Redis" lives.
- **Local Disk (SSD):** Slower (milliseconds) but huge and permanent.
- **Network / CDN:** Slowest (10-200 milliseconds) due to the geography of the internet.
- **Volatile vs Non-Volatile:** Caches that die when the power is pulled!

### Research Topics
- "The L1, L2, L3 Cache Hierarchy explained"
- "Latency numbers every programmer should know (Jeff Dean's list)"
- "Why the CPU uses 3 different caches (L1-L3)"
- "The performance gap between RAM and SSD"

---

### The Practical Challenge

**Part 1: The "Waiting" Math**
1. Research **Jeff Dean's Latency Numbers**. 
   - L1 Cache: 0.5 ns.
   - RAM: 100 ns. (200x slower).
   - SSD: 100,000 ns. (1,000x slower than RAM!).
   - Across the Atlantic (NYC -> London): 150,000,000 ns.
2. If L1 were "Heartbeat" (1 second), how long would "Going to London" be? (Answer: ~5 years!).
3. Discuss: Why does a 0.1ms delay in a database query matter to a user in Japan?

**Part 2: The Browser Hierarchy**
1. Open Chrome DevTools -> Application -> Storage.
2. Identify:
   - **Memory Cache:** (Scripts loaded for the current page).
   - **Disk Cache:** (Images/CSS saved from yesterday).
   - **Local Storage:** (Small "Key-Value" data for the app).

**Part 3: Identifying the "Level"**
1. Where should you cache:
   - "The current result of 1+1" (Answer: CPU Register / L1).
   - "A 1GB User Profile" (Answer: RAM / SSD).
   - "A 10MB JPG image of a kitten" (Answer: CDN / Disk Cache).

**Part 4: Real-world check**
1. On Mac: `sysctl -a | grep cache`. On Linux: `lscpu`.
2. Find your CPU's L1, L2, and L3 cache sizes. 
3. Discuss: Why is L1 only a few **Kilobytes** while L3 is many **Megabytes**? (Answer: Cost and physical distance on the silicon chip).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The False Hit. If you don't use a "Hash" or unique key, your cache might give User A the private profile of User B.
- **Gotcha 2:** The "Cold Cache." When you first deploy your app, every single request will be slow because the cache is empty (The "Thundering Herd" problem).

### Reflection Question
Why is "Wait time" (Latency) the #1 killer of application performance, rather than "Slow CPU"? (Answer: Because a modern CPU can do 1,000,000 actions while it's waiting for ONE database packet from the network).
