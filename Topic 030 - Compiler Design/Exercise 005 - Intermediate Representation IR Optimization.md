# Exercise 005 - Intermediate Representation (IR) & Optimization

### Objective
Simplify and Speed up. Master **Intermediate Representation (IR)**. Learn why compilers translate code into a "Middle" language (like **LLVM IR**) before going to machine code. Understand how **Compiler Optimizations** (like "Constant Folding" or "Dead Code Elimination") make your code run faster without you changing a line of text.

### Core Concepts to Master
- **Intermediate Representation (IR):** A low-level, language-independent version of your code (e.g., Three-Address Code).
- **Constant Folding:** Evaluating `2 + 3` into `5` at compile time so the CPU doesn't have to do it at runtime.
- **Dead Code Elimination:** Removing code that can never be reached (e.g., code after a `return`).
- **Inlining:** Replacing a function call with the actual body of the function to save the overhead of starting a new stack frame.
- **LLVM:** The industry-standard "Backend" for compilers (used by Clang, Rust, Swift).

### Research Topics
- "What is LLVM IR and how to read it?"
- "Compiler optimization techniques: Constant folding, loop unrolling"
- "The cost of 'Inlining' and when the compiler says No"

---

### The Practical Challenge

**Part 1: The Three-Address Code (TAC)**
1. Imagine the high-level code: `x = (y + z) * 10`.
2. Translate this to **Three-Address Code**:
   - `temp1 = y + z`
   - `x = temp1 * 10`
3. Discuss: Why is this simpler for a computer to process than the nested expression?

**Part 2: The Optimizer at Work**
1. Identify the optimization in this code:
   - **Original:** `var PI = 3.14; var circ = PI * 2 * 10;`
   - **Optimized:** `var circ = 62.8;`
2. This is called **Constant Folding**. How much CPU work did the compiler just save?

**Part 3: Dead Code Hunting**
1. Look at this code:
   ```
   func do_thing() {
     return 5;
     print("Hello!"); // This line
   }
   ```
2. Explain why the compiler will completely delete the `print` line from the final binary.

**Part 4: Reading LLVM (Conceptual)**
1. Research what LLVM IR looks like (e.g., `@x = global i32 10`).
2. Discuss why writing a compiler that targets "LLVM IR" is better than writing one that targets "M1 Mac Code" and "Intels Code" and "iPhone Code" separately. (Hint: LLVM handles the hardware generation for you).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Changing the Meaning. An optimizer must never change the *result* of the code. If it "Optimizes" a bug away, it is a bad optimizer.
- **Gotcha 2:** The "Optimization Level" (-O0, -O2, -O3). Higher levels of optimization make your code faster but take much longer to compile and make "Debugging" (using a debugger) harder because the code structure has been mangled.

### Reflection Question
Why do most compilers turn off optimizations (-O0) during development and only turn them on (-O3) for the final production build?
