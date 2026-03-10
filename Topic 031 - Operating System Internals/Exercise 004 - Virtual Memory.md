# Exercise 004 - Virtual Memory & Swap

### Objective
The illusion of infinite RAM. Master **Virtual Memory**. Learn how the OS allows programs to use more memory than physically exists in the computer by using the **Disk (Swap)** as an overflow tank. Understand **Page Faults** and the impact of slow disk access on program speed.

### Core Concepts to Master
- **Virtual Memory Address Space:** Every process thinks it has the entire memory range (e.g., 0 to 2^64) all to itself.
- **MMU (Memory Management Unit):** The hardware component that does the high-speed translation from Virtual -> Physical.
- **Page Fault:** What happens when you try to access data that is on the Disk but not currently in the RAM.
- **Swap / Pagefile:** The area on your SSD/HDD used to store "overflow" memory.

### Research Topics
- "Why use Virtual Memory?"
- "The physical location of the MMU"
- "Thrashing: Why your computer gets hot and slow"
- "The LRU (Least Recently Used) page replacement algorithm"

---

### The Practical Challenge

**Part 1: The "Dirty" Page Fault**
1. Research the steps of a Page Fault:
   - Trap to OS.
   - Find frame on disk.
   - Find free frame in RAM (or evict someone else).
   - Copy disk -> RAM.
   - Update Page Table.
   - Resume process.
2. Discuss: Why does a Page Fault take 1,000,000x longer than a normal RAM read?

**Part 2: Configuring Swap**
1. On Linux, check swap with `swapon --show`. 
2. On Mac, check the `/var/vm/` directory for `swapfile` entries.
3. Discuss: If you have a super-fast NVMe SSD, is "Swap" as painful as it was in the HDD days?

**Part 3: The Eviction Policy**
1. You have 3 slots in RAM.
2. Sequence of pages accessed: `1, 2, 3, 4, 1, 2`.
3. Use the **FIFO** (First In First Out) strategy to track which pages are kicked out.
4. Now use the **LRU** (Least Recently Used) strategy. 
5. Compare the number of "Page Faults" for each.

**Part 4: Measuring Memory Pressure**
1. Write a script that allocates 1GB of memory in a loop. 
2. Use `htop` or `Activity Monitor`. 
3. Watch the "Compressed Memory" or "Swap Used" increase. 
4. Stop before the computer crashes!

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Memory Leaks vs Swap. If your app has a memory leak, it will eventually push EVERY other app on the computer into the "Swap zone," making the entire OS unusable.
- **Gotcha 2:** Disabling Swap. Some people disable swap to "save disk health." Discuss why this is dangerous and usually results in "OOM Killer" crashes.

### Reflection Question
How does Virtual Memory act as a security barrier between two different apps (like a Bank app and a Game app) running on the same machine?
