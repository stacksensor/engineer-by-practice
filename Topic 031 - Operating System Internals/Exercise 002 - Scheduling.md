# Exercise 002 - Scheduling Algorithms

### Objective
Master the "Traffic Controller" of the CPU. Understand how the Operating System decides which process gets to run on the CPU next. Learn about **Round Robin**, **Priority Scheduling**, and **Multi-level Feedback Queues**, and understand the trade-offs between **Fairness** and **Throughput**.

### Core Concepts to Master
- **The Scheduler:** The OS component that manages the "Ready Queue."
- **Time Slice (Quantum):** The fixed amount of time a process is allowed to run before being interrupted.
- **Preemptive vs Non-preemptive:** Can the OS "force" a process off the CPU, or must the process volunteer to leave?
- **Starvation:** What happens when a low-priority process never gets a turn because high-priority processes keep arriving.

### Research Topics
- "First-Come, First-Served (FCFS) limitations"
- "Shortest Job Next (SJN)"
- "Round Robin (RR) and the importance of the time quantum"
- "Multi-level Feedback Queues (Linux O(1) and CFS schedulers)"

---

### The Practical Challenge

**Part 1: The Wait Time Math**
1. Imagine 3 jobs: Job A (20ms), Job B (5ms), Job C (10ms).
2. Calculate the "Average Wait Time" using FCFS (Order: A, B, C).
3. Calculate it again using SJN (Order: B, C, A).
4. Discuss: Why does changing the order improve the average wait time?

**Part 2: Round Robin Simulation**
1. Using 3 jobs (A: 20ms, B: 5ms, C: 10ms) and a Time Slice of 5ms.
2. Trace the execution:
   - 0-5ms: A runs (15 left)
   - 5-10ms: B runs (Done!)
   - 10-15ms: C runs (5 left)
   - ...continue.
3. Discuss: What happens to "Wait Time" if the slice is too small? (Hint: Context switching overhead).

**Part 3: Priority Starvation**
1. Design a system where "High Priority" jobs skip the line.
2. Discuss: If 100 high-priority jobs arrive every second, what happens to the 1 low-priority job that arrived this morning?
3. Research **"Aging"** as a solution to starvation.

**Part 4: Real-world check**
1. Research the **CFS (Completely Fair Scheduler)** in the Linux Kernel.
2. How does it use a "Red-Black Tree" to manage tasks?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Convoy Effect. A slow job (like a massive video export) blocks small jobs (like a mouse click) in FCFS systems.
- **Gotcha 2:** CPU Bound vs IO Bound. Some processes just need to "wait" (IO). The scheduler should put them to sleep so they don't waste CPU time.

### Reflection Question
Why doesn't the OS just give every process "Infinite" time on the CPU? (Answer: Preemption and the illusion of multi-tasking).
