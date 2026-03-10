# Exercise 001 - Build Systems: Compile-to-Binary

### Objective
Create the output. Master the concept of **Build Systems**—the bridge between your code (human-readable text) and the final "Product" (machine-readable binary). Learn the steps of **Compilation**, **Linking**, and **Packaging**, and understand how to use tools like `make`, `gcc`, or `cargo` to automate this process.

### Core Concepts to Master
- **Compilation:** Turning a `.c`, `.cpp`, or `.rs` file into an "Object file" (`.o`).
- **Linking:** Combining multiple object files and 3rd-party libraries into one final "Executable" (`.exe` or binary).
- **In-place vs. Build Directory:** Why we use a `build/` or `dist/` folder to keep the source code clean.
- **The Makefile:** The classic tool for build automation (the "How-to-build" recipe).
- **Cargo (Rust):** A modern build system that manages dependencies AND builds the code in one step.

### Research Topics
- "What is a compiler? (GCC vs Clang vs MSVC)"
- "The steps of a C++ build: Preprocessing, Compiling, Linking"
- "GNU Make: Simple examples for beginners"
- "Static vs Dynamic Linking"

---

### The Practical Challenge

**Part 1: The "Simple" Compile (C or C++)**
1. Create a file `hello.c`: `#include <stdio.h>\nint main() { printf("hi"); }`.
2. Compile it manually: `gcc hello.c -o myapp`.
3. Discuss: What did the computer just do to your text file? 
4. (Answer: Transformed it into a CPU-native binary).

**Part 2: The "Linker" Error**
1. Create a second file `utils.c` with a function `print_hi()`. 
2. Use it in `main.c` but DON'T compile `utils.c`.
3. Try to build: `gcc main.c -o myapp`.
4. Observe the "Undefined Reference" error. This is a **Linker Error**. 
5. Fix it: `gcc main.c utils.c -o myapp`.

**Part 3: The "Make" Automation**
1. Research the command `make`. 
2. Create a `Makefile` that builds your app.
3. Discuss: Why is `make` better than typing the `gcc` command every time? 
4. (Answer: `make` only rebuilds the files you CHANGED, saving time in large projects).

**Part 4: Identifying the "Chain"**
1. Research the **Toolchain** for your favorite language (e.g., Node.js uses `tsc` for TypeScript; Rust uses `rustc`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Path Hell. If your build system can't "find" a library that you installed, it will fail. Always check your `PATH` or `LD_LIBRARY_PATH`.
- **Gotcha 2:** The "Dirty" Build. Sometimes old object files stick around and cause weird bugs. Always try a `clean` (e.g., `make clean` or `cargo clean`) if you run into an "Impossible" error.

### Reflection Question
Why are "Dependency Managers" (like NPM or Cargo) now integrated into modern Build Systems instead of being separate separate tools? (Answer: To ensure the "Build" environment is identical on every machine).
