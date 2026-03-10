# Exercise 006 - Code Generation & Target Architecture

### Objective
Speak the machine's language. Master **Code Generation**, the final stage of a compiler. Learn how the high-level AST or IR is finally translated into specific **Register** movements and **Assembly/Machine Code** instructions for a particular CPU (x86_64 or ARM).

### Core Concepts to Master
- **Target Architecture:** The specific hardware the code will run on (e.g., Apple M3 is ARM; Google Cloud is usually Intel x86).
- **Registers:** Tiny, ultra-fast storage locations inside the CPU (`rax`, `rbx`, `rsp`).
- **Instruction Set Architecture (ISA):** The "Vocabulary" of the CPU (e.g., `MOV`, `ADD`, `JMP`, `CALL`).
- **Stack Management:** How the compiler generates code to create and destroy stack frames for functions.
- **Register Allocation:** The "Puzzle" of deciding which variables stay in the fast registers and which are "Spilled" to the slower RAM.

### Research Topics
- "Introduction to x86_64 Assembly for beginners"
- "How compilers generate assembly code"
- "Register allocation and spilling"
- "Machine code vs. Assembly vs. High-level language"

---

### The Practical Challenge

**Part 1: Reading Assembly**
1. Use the [Compiler Explorer (godbolt.org)](https://godbolt.org/).
2. Write a simple function in C: `int square(int num) { return num * num; }`.
3. Choose the "x86-64 gcc" compiler.
4. Look at the output. Identify the `IMUL` (Multiplication) instruction.
5. Discuss: Even if you don't know assembly, how can you "See" the math happening?

**Part 2: The Register Puzzle**
1. Imagine a CPU with only 2 Registers: `RegA` and `RegB`.
2. You need to do: `(x + y) * (z + w)`.
3. Plan the movement:
   - Load `x` and `y` -> Add them -> Save to `RegA`.
   - Load `z` and `w` -> Add them -> Save to `RegB`.
   - Multiply `RegA` and `RegB`.
4. Discuss: What if you had 4 additions to do? Where would the extra results go? (Hint: The Stack).

**Part 3: Branching (If/Else)**
1. Research how an `if` statement is translated into a **Jump (`JMP`)** instruction in assembly.
2. Discuss why "GOTO" is considered bad in high-level code, but is the *only* way the CPU handles logic at the low level.

**Part 4: Linking (Conceptual)**
1. Research the difference between a **Compiler** and a **Linker**.
2. Discuss: If your code uses a library (like `math.h`), the compiler leaves a "Placeholder" and the Linker "Stitches" the two parts together at the end.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Architecture Mismatch. If you try to run an "x86" binary on an "ARM" Mac (without Rosetta), it will fail with "Bad CPU type."
- **Gotcha 2:** Calling Conventions. Different operating systems have different "Rules" for which registers are used to pass data to functions. If the compiler gets this wrong, the app will crash instantly.

### Reflection Question
Why is the "Code Generation" phase the most repetitive and tedious part of writing a compiler from scratch?
