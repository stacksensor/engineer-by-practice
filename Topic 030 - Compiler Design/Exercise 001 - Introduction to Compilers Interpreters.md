# Exercise 001 - Introduction to Compilers & Interpreters

### Objective
Look under the hood of your favorite language. Understand the difference between **Compilers** (translated to machine code upfront) and **Interpreters** (translated line-by-line during execution). Master the standard "Compiler Pipeline"—from high-level syntax down to low-level execution—and understand how the computer actually "Reads" code.

### Core Concepts to Master
- **The Compiler Pipeline:** 
  1. **Lexical Analysis:** (Tokens).
  2. **Syntax Analysis:** (AST).
  3. **Semantic Analysis:** (Meanings/Types).
  4. **Intermediate Representation (IR):** (Optimization).
  5. **Code Generation:** (Target language/Machine code).
- **AOT vs. JIT:** 
  - **Ahead-of-Time (AOT):** C++, Rust, Go.
  - **Just-in-Time (JIT):** Java (JVM), JavaScript (V8).
- **Interpreted:** Python, Ruby (mostly).

### Research Topics
- "The Dragon Book (Compilers: Principles, Techniques, and Tools)" (Just the overview!)
- "How does the V8 engine work?"
- "The steps of a compiler explained for beginners"

---

### The Practical Challenge

**Part 1: The Translator Roleplay**
1. Imagine you have a shopping list in English: `buy 2 apples`.
2. **The Compiler Way:** You translate the whole list to French, print it on paper, and give it to a French speaker.
3. **The Interpreter Way:** You read the first item in English, tell the French speaker what it is, wait for them to buy it, then read the second item.
4. Discuss: Which way is "Faster" to start? Which way is "More efficient" for a 1,000-item list?

**Part 2: Investigating Your Tools**
1. Run `python --version` and `gcc --version` (if installed).
2. Research: When you run a `.py` file, what is the output? (Answer: Bytecode in `__pycache__`).
3. When you run `gcc main.c`, what is the output? (Answer: A binary file like `a.out`).
4. Use the `file` command to inspect the output: `file a.out`. Identify that it is "Executable" and specific to your "Architecture" (e.g., x86_64 or ARM).

**Part 3: From Text to Trees (Conceptual)**
1. Look at this code: `x = 10 + 5 * 2`.
2. Discuss: Why does the computer need to "Tree-ify" this to know that `5 * 2` happens *before* adding `10`?
3. Research what an **AST (Abstract Syntax Tree)** looks like for this expression.

**Part 4: The Bytecode Middleman**
1. Research the **Java Virtual Machine (JVM)** or the **LLVM** project.
2. Discuss why modern languages compile to a "Middle" language (Intermediate Representation) instead of going directly to Machine Code.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The JIT "Warm up." JIT languages (like JS) can be slow for the first few seconds while the engine "learns" which parts of your code are "hot" and should be optimized.
- **Gotcha 2:** Target Lock-in. An AOT compiler produces code for a specific OS and CPU. A binary compiled for Windows will not run on a Mac.

### Reflection Question
Why are "Compiled" languages generally faster than "Interpreted" languages, but "Interpreted" languages are generally easier for beginners to learn and debug?
