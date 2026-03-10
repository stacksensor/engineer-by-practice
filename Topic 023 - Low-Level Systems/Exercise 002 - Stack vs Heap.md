# Exercise 002 - Stack vs Heap (Memory Management)

### Objective
Master where data lives. Learn the critical difference between the **Stack** (fast, small, automatically managed storage for local variables) and the **Heap** (large, slower, manually or garbage-collected storage for objects and dynamic data). Understand why "Memory Leaks" happen and how the computer stays organized as functions are called and returned.

### Core Concepts to Master
- **The Stack:** 
  - Follows "Last In, First Out" (LIFO).
  - Stores local variables and function parameters.
  - Automatically cleaned up when a function returns.
  - Extremely fast (stays in CPU cache).
- **The Heap:**
  - Used for large pieces of data (objects, arrays) that need to live longer than a single function call.
  - Requires manual management (C/C++) or a Garbage Collector (JS/Java/Python).
  - Can be fragmented.
- **Stack Overflow:** What happens when you have an infinite recursive function that uses up all the stack space.
- **Memory Leak:** When you allocate memory on the heap but lose the variable (pointer) pointing to it, making it impossible to free that memory.

### Research Topics
- "Difference between stack and heap memory"
- "How recursion uses the stack"
- "What is a segmentation fault (segfault)?"
- "Memory allocation: malloc vs free"

---

### The Practical Challenge

**Part 1: Visualizing the Stack**
1. Imagine this code:
   ```
   func A():
     var x = 10
     B()
   func B():
     var y = 20
   ```
2. Sketch the Stack:
   - When B is called, a "Stack Frame" for B is added on top of A.
   - When B returns, its frame is "popped" and `y` is instantly erased from memory.
   - Now, explain why you cannot access `y` from inside func A.

**Part 2: The Heap Invitation**
1. Imagine you want to create an array of 1 million integers that needs to be shared between many different parts of your program.
2. Discuss: Why can't you store this on the Stack? (Hint: Stack size is usually limited to 1-8 MB).
3. Research how languages like C++ use the `new` keyword to put this array on the Heap.

**Part 3: The Ghost in the Machine (Memory Leak)**
1. In a language without a garbage collector (like C):
   - You request 1MB of memory on the Heap (`malloc`).
   - You use the memory.
   - Your function returns but you *forgot* to call `free()`.
2. Discuss what happens to the RAM on your computer if this function runs 1,000 times per second.

**Part 4: Stack vs Heap Performance**
1. Research why accessing data on the Stack is almost always "Zero Latency" for the CPU, while searching for a memory address on the Heap can trigger a "Cache Miss."
2. Explain how this affects the performance of high-level languages like Java or Python which put almost everything on the Heap.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Dangling Pointers. If you free a piece of memory on the heap but your code still tries to read from that address, your program will crash with a "Segfault."
- **Gotcha 2:** Deep Recursion. If you see a "Maximum call stack size exceeded" error in JavaScript, it means your stack has grown so large it hit the OS limit.

### Reflection Question
Why do languages like JavaScript and Python use a "Garbage Collector" to manage the Heap instead of making the programmer do it manually?
