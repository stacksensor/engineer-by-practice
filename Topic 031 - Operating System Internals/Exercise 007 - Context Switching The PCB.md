# Exercise 007 - Context Switching & The PCB

### Objective
Freeze and Resurrect. Master **Context Switching**—the act of saving the state of one process so another can run, and later restoring it exactly where it left off. Learn about the **PCB (Process Control Block)** and understand why context switching is the "Hidden Cost" of running many apps at once.

### Core Concepts to Master
- **The Context:** The current values of all CPU registers, the Program Counter (where you are), and the Stack Pointer (where your data is).
- **PCB (Process Control Block):** The "Save Game" file for a process stored in the Kernel's memory.
- **Save State -> Schedule -> Load State:** The 3-step dance of a context switch.
- **Cache Invalidation:** Why a context switch is slow (it's not just the memory move; it's the fact that the CPU L1/L2 caches are now "Cold").

### Research Topics
- "What is a Process Control Block (PCB)?"
- "The steps of a context switch in Linux"
- "Hardware support for context switching (Register banking)"
- "Voluntary vs Involuntary context switches"

---

### The Practical Challenge

**Part 1: Identifying the "Context"**
1. Look at a CPU register list (e.g., `RAX`, `RBX`, `RIP`, `RSP`).
2. Why is `RIP` (the instruction pointer) the most important one to save? (Answer: Because it's the "You Are Here" marker).

**Part 2: Measuring Switches (Tooling)**
1. On Linux, run `vmstat 1`. Look at the `cs` (Context Switches) column.
2. On Mac, run `top -l 1 | grep "context switches"`.
3. Open 20 Chrome tabs and 5 other apps. Observe how the `cs` number increases.
4. If the number is 10,000 per second, calculate how much "Total time" is wasted if each switch takes 1 microsecond.

**Part 3: Voluntary vs Involuntary**
1. If Process A finishes its time slice and the OS kicks it off, is that Voluntary or Involuntary? (Answer: Involuntary).
2. If Process A calls `sleep(5)`, is it Voluntary or Involuntary? (Answer: Voluntary).
3. Research: Which type is "easier" on the CPU?

**Part 4: The PCB Structure**
1. Research the `struct task_struct` in the Linux Kernel source code. 
2. Identify 3 things stored there that are NOT CPU registers (e.g., `priority`, `pid`, `state`, `open_files`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Too Many Threads. If you create 5,000 threads for 5,000 users, the CPU might spend 50% of its time just "Switching" between them and 50% doing real work.
- **Gotcha 2:** Affinty. Sometimes the OS tries to keep a process on the "Same CPU core" during a switch to keep the L1/L2 cache "Warm." This is called **CPU Affinity**.

### Reflection Question
How does Context Switching allow a single-core CPU to give 50 different users the "Illusion" that they are all using the computer simultaneously?
