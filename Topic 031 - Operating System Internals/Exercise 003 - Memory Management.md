# Exercise 003 - Memory Management & Paging

### Objective
Organize the bytes. Master how the OS manages physical RAM. Learn about **Contiguous Allocation**, **Fragmentation**, and the breakthrough of **Paging**—which allows blocks of memory to be scattered throughout physical RAM while appearing solid to your code.

### Core Concepts to Master
- **The RAM:** Physical hardware addresses.
- **Fragmentation:**
  - **External:** Gaps of free space between allocated blocks.
  - **Internal:** Wasted space inside a large block allocated to a small variable.
- **Pages (Software) & Frames (Hardware):** Dividing memory into fixed-size blocks (usually 4KB).
- **Page Table:** The "Map" that translates a logical page to a physical frame.

### Research Topics
- "Contiguous vs Non-contiguous memory allocation"
- "Memory Fragmentation problems"
- "Fixed-size partitions vs Dynamic partitions"
- "The Page Table Entry (PTE)"

---

### The Practical Challenge

**Part 1: The Fragmentation Puzzle**
1. You have 100MB of RAM.
2. Alloc A (40MB), Alloc B (40MB). 20MB remains free.
3. Free Alloc A. Now 20MB at the start and 20MB at the end are free.
4. Try to allocate 30MB. Even though you have 40MB "total" free, you can't fit 30MB in one piece.
5. This is **External Fragmentation**. How does "Paging" solve this?

**Part 2: The Page Map**
1. Imagine 4KB pages.
2. Your program needs 10KB. 
3. How many pages does it need? (Answer: 3).
4. How much space is wasted in the last page? (Answer: 2KB). This is **Internal Fragmentation**.

**Part 3: The Translation (Math)**
1. A Logical Address consists of `(Page Number, Offset)`.
2. Offset equals 12 bits (for 4KB pages).
3. If Page 5 maps to Frame 100, calculate the hardware address if the offset is 50.

**Part 4: Inspecting Memory (Tooling)**
1. Use `vm_stat` on Mac or `free -m` on Linux.
2. Look for "Page Ins" and "Page Outs." 
3. Discuss: Why does the OS read/write memory in blocks (pages) rather than individual bits?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Page Table Size. If you have 4GB of RAM and 4KB pages, the "Map" itself can become very large. Modern OSs use "Multi-level Page Tables" to solve this.
- **Gotcha 2:** The "Thrashing" state. If the CPU spends 99% of its time moving pages in and out of RAM and 1% doing work, the computer "freezes."

### Reflection Question
Why is "Paging" considered one of the most important inventions in computer science for software reliability?
