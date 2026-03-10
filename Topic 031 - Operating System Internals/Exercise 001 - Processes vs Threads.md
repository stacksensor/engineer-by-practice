# Exercise 001 - Processes vs. Threads

### Objective
Understand the fundamental unit of execution. Master the difference between **Processes** (independent, isolated memory) and **Threads** (shared memory within a process). Learn when to use each based on overhead, communication speed, and safety.

### Core Concepts to Master
- **Process:** An instance of a running program with its own address space, file descriptors, and security context.
- **Thread:** A "lightweight" execution unit within a process. Threads share the process's heap but have their own stack.
- **Inter-Process Communication (IPC):** Why processes need mechanisms like Pipes, Sockets, or Shared Memory to talk.
- **Race Conditions:** Why threads are dangerous (memory sharing) while processes are safer (isolation).

### Research Topics
- "Process vs Thread memory model"
- "The cost of creating a process vs a thread"
- "What is a Zombie Process?"
- "Thread-local storage (TLS)"

---

### The Practical Challenge

**Part 1: The Parent-Child Process (fork)**
1. In C or Python, use `os.fork()`.
2. Observe how the memory is "Copied" initially.
3. Update a variable in the child process. Check if it changed in the parent. (Spoiler: It won't).
4. Identify the `PID` (Process ID) of both.

**Part 2: The Shared Heap (Threads)**
1. Using Python `threading` or C `pthreads`, create two threads.
2. Have them both update a global shared variable.
3. Observe what happens without a "Lock" (Mutex).
4. Does the parent process still see the changes? (Spoiler: Yes).

**Part 3: Measuring Creation Time**
1. Write a script to create 1,000 processes. Measure how long it takes.
2. Write a script to create 1,000 threads. Measure how long it takes.
3. Compare the overhead.

**Part 4: Zombie Hunt**
1. Create a child process that finishes instantly, while the parent sleeps for 60 seconds.
2. Use `ps aux | grep Z` to find the "Zombie" process.
3. Research: Why does the OS keep finished processes as zombies? (Answer: To save the exit status).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Deadlock. If Thread A waits for Thread B, and Thread B waits for Thread A, the process freezes.
- **Gotcha 2:** The Python GIL. In Python, threads cannot run on multiple CPU cores simultaneously for CPU-bound tasks. Use `multiprocessing` for that.

### Reflection Question
Why are web browsers like Chrome designed to use one "Process" per tab instead of just a "Thread" per tab?
