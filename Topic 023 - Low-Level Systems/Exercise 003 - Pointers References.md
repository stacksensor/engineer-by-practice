# Exercise 003 - Pointers & References

### Objective
Master the "Address of Data." Learn how to interact directly with memory addresses using **Pointers** (C/C++) and **References**. Understand why passing by reference is more efficient for large data than passing by value, and learn the risks of "pointer arithmetic" and memory corruption.

### Core Concepts to Master
- **Memory Address:** The unique identifier (e.g., `0x7ffd9`) of a specific byte on your RAM sticks.
- **The Pointer (`*`):** A variable that stores a memory address instead of a value. 
- **Dereferencing:** Using a pointer to "Go to" that address and read the value inside.
- **Address-of Operator (`&`):** Getting the address of a regular variable.
- **Null Pointer:** A pointer that points to address `0`. Trying to read it causes a crash.
- **Pass-by-Value vs. Pass-by-Reference:** Copying the entire data into a function vs. just sending the "Address" of the data.

### Research Topics
- "What are pointers in C for beginners?"
- "Pointer vs Reference differences"
- "Visualizing memory addresses in C++"

---

### The Practical Challenge

**Part 1: The Address Lab**
1. Imagine two variables in memory: `Age = 25` (at address 0x1) and `Salary = 5000` (at address 0x2).
2. Create a Pointer named `p` and set its value to `0x1`. 
3. If you "Dereference" `p`, what value do you get? 
4. If you change the value at that address to `26`, what is the value of the original `Age` variable now?

**Part 2: Pass by Reference (Efficiency)**
1. Imagine an object representing a High-Resolution Photo (100MB).
2. **Technique A (Pass by Value):** When you send the photo to a "Filter" function, the computer copies all 100MB of data to a new part of memory.
3. **Technique B (Pass by Reference):** You send the "Memory Address" (8 bytes) of the photo to the function.
4. Calculate the memory savings of Technique B. 

**Part 3: The Dangerous Math (Pointer Arithmetic)**
1. In C, you can take a pointer and add `1` to it: `ptr + 1`. This moves it to the next memory address.
2. Discuss: If you have an Array of 5 items, what happens if you add `6` to the pointer and try to read from that address? (Hint: You are reading "garbage" or data belonging to a different app).

**Part 4: The Shared State Problem**
1. If two different functions have a pointer to the same object on the heap, and Function A deletes (frees) the object, what happens when Function B tries to access it?
2. Research how "Smart Pointers" (like `shared_ptr` in C++) try to solve this using Reference Counting.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Uninitialized Pointers. If you create a pointer but don't set its address, it contains a random value from a previous program. This is extremely dangerous.
- **Gotcha 2:** The "Segfault" on Null. Always check `if (ptr != NULL)` before trying to read from a pointer.

### Reflection Question
Why are pointers considered the primary reason why C and C++ programs are harder to write safely than Java or Python programs?
