# Exercise 001 - The CPU, Memory & OS Basics

### Objective
Look under the hood. Move away from high-level abstractions to understand the physical and logical foundations of computing. Learn how the CPU executes instructions, how the Operating System manages hardware for multiple processes, and how data moves between Registers, Cache, and RAM.

### Core Concepts to Master
- **The CPU Cycle:** Fetch -> Decode -> Execute.
- **Registers:** Tiny, ultra-fast memory inside the CPU.
- **The Memory Hierarchy:** Understanding the significant speed differences between L1/L2 Cache, RAM (Main Memory), and Disk (SSD/HDD).
- **System Calls (syscalls):** The "Bridge" between user space (your code) and kernel space (the OS).
- **Virtual Memory:** How the OS gives every process the "Illusion" that it has access to the entire range of system RAM.

### Research Topics
- "How do computer processors work? (Beginners guide)"
- "CPU Cache: L1, L2, L3 explained"
- "What is the difference between User Space and Kernel Space?"
- "The physical architecture of a von Neumann machine"

---

### The Practical Challenge

**Part 1: The Speed of Light (Conceptual)**
1. Research "Latency numbers every programmer should know."
2. Compare the time taken for:
   - A CPU Register access.
   - A Main Memory (RAM) access.
   - A Disk (SSD) access.
   - A Network packet across the Atlantic.
3. Discuss: Why does a programmer care about "L1 Cache Hits" if they are writing in a high-level language like Python?

**Part 2: Investigating System Calls**
1. Learn how to use a tool like `strace` (Linux) or `dtruss` (Mac) to monitor system calls.
2. Run a simple command like `ls`. 
3. Observe how many intermediate steps the OS takes: `openat`, `readdir`, `write` (to the terminal).
4. Discuss: No matter what language you use, every time you print to a screen or save a file, you are talking to the OS via a System Call.

**Part 3: CPU Context Switching**
1. Run `top` or `htop`. Look at the number of "Context Switches" per second.
2. Research what happens when the CPU stops running App A to run App B.
3. Why is having 10,000 active threads usually slower than having 10 active threads?

**Part 4: Binary & Hexadecimal Basics**
1. Learn how to convert Decimal numbers (0-10) to Binary (0-1) and Hexadecimal (0-F).
2. Why is Hexadecimal used instead of Binary when describing memory addresses in computer science?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Virtual Memory" confusion. Just because your code thinks a value is at address `0x123A`, it doesn't mean it's at that physical location on your RAM sticks. The OS maps these addresses dynamically.
- **Gotcha 2:** 32-bit vs 64-bit limits. A 32-bit system can only address about 4GB of RAM (2^32). A 64-bit system can address almost 18 quintillion bytes (2^64).

### Reflection Question
If memory access is so much slower than CPU cycles, how do techniques like "Prefetching" help keep the CPU busy?
