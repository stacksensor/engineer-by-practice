# Exercise 006 - Concurrency & Threads

### Objective
Master parallelism without the crashes. Learn how to use **Threads** to perform multiple tasks simultaneously, and explore the classic "Dangers" of concurrency like **Race Conditions** and **Deadlocks**. Learn how low-level synchronization primitives like **Mutexes** and **Atomics** keep your data consistent across threads.

### Core Concepts to Master
- **Processes vs. Threads:** A Process has its own memory space; Threads share the same memory space.
- **Race Condition:** When two threads try to update the same memory at the exact same time, leading to unpredictable results (e.g., `10 + 1 + 1 = 11` instead of `12`).
- **Mutex (Mutual Exclusion):** A "Lock" that ensures only one thread can access a piece of data at a time.
- **Atomic Operations:** CPU-level instructions that perform an action (like an increment) as a single, uninterruptible step.
- **Deadlock:** When Thread A is waiting for a lock held by Thread B, while Thread B is waiting for a lock held by Thread A. Both are frozen forever.

### Research Topics
- "Multi-threading for beginners"
- "What is a race condition example?"
- "Rust Fearless Concurrency: How the compiler stops data races"
- "Mutex vs Semaphore vs Atomic"

---

### The Practical Challenge

**Part 1: The Counter Race (Conceptual or Code)**
1. Imagine a global variable `counter = 0`.
2. Start 2 threads. Each thread runs a loop 1,000 times: `counter = counter + 1`.
3. If the threads were truly parallel, you expect `counter = 2000`.
4. Run the code. Observe that the result is often much less than 2000 (e.g., 1854).
5. Explain why this happens. (Line 1: Thread A reads 10. Line 2: Thread B reads 10. Line 3: Thread A writes 11. Line 4: Thread B writes 11. One increment was "Lost").

**Part 2: Fixing with a Mutex**
1. Wrap the counter in a **Mutex**. 
2. Ensure each thread must `lock()` the mutex before incrementing and `unlock()` after.
3. Run the code again. Verify the result is exactly `2000`.
4. Discuss the performance cost of locking. Why is this slower than the "Race" version?

**Part 3: The Deadlock Trap**
1. Create two Mutexes: `LockA` and `LockB`.
2. Thread 1 locks A, then tries to lock B.
3. Thread 2 locks B, then tries to lock A.
4. Run both and observe the system freeze. This is a **Deadlock**.
5. Discuss: How can you prevent this? (Hint: Always lock your mutexes in the same order across the entire app).

**Part 4: Fearless Concurrency in Rust**
1. Research how **Rust's Ownership and Borrowing** rules prevent the "Counter Race" from even compiling.
2. Explain how the compiler forces you to use a Thread-Safe wrapper (like `Arc<Mutex<T>>`) before it allows you to send data to another thread.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Context Switch Overhead. Creating 10,000 threads for 10,000 small tasks is very slow. Use a "Thread Pool" (like `rayon` or `tokio`) to reuse a small number of threads for many tasks.
- **Gotcha 2:** Starvation. If "Priority" threads keep hogging a lock, "Low Priority" threads might never get to run.

### Reflection Question
Why are "Atomics" faster than "Mutexes" for simple counters, but useless for complex data structures like a list or a map?
