# Exercise 004 - Introduction to Rust (Safety & Memory)

### Objective
Learn the modern way of "Safe" low-level systems programming. Explore **Rust**, a language that provides the performance of C/C++ but uses a unique compiler system to guarantee memory safety without needing a slow Garbage Collector. Understand why Rust is becoming the standard for high-performance, secure infrastructure.

### Core Concepts to Master
- **Memory Safety without GC:** How the Rust compiler checks your code at "Compile Time" to prevent memory leaks, segfaults, and data races.
- **The Borrow Checker:** The specific part of the Rust compiler that enforces strict rules about how memory is shared.
- **Immutability by Default:** In Rust, variables are locked by default (`let x = 5`). You must explicitly say `mut` (`let mut x = 5`) if you want to change it.
- **Strong Typing:** Rust's strict type system that catches errors before your program even runs.

### Research Topics
- "What makes Rust unique?"
- "Installing Rust using rustup"
- "Rust vs C++: Memory safety comparison"
- "Helpful error messages in Rust"

---

### The Practical Challenge

**Part 1: Setting up the Environment**
1. Install Rust using the official installer: `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`.
2. Verify the installation: `rustc --version` and `cargo --version`.
3. Create your first project: `cargo new hello_rust`.
4. Open `src/main.rs`. Notice the `fn main()` entry point.

**Part 2: The "Immutability" Lesson**
1. In `main.rs`, write:
   ```rust
   let x = 10;
   x = 20;
   println!("{}", x);
   ```
2. Run `cargo run`. Observe the compiler error. 
3. Read the error message carefully. Notice how it suggests adding `mut`.
4. Fix the code: `let mut x = 10;` and run again.

**Part 3: Typing & Consistency**
1. Try to add a string to an integer: `let sum = 10 + "20";`.
2. Observe how the compiler refuses to run the code. 
3. Research how to "Parse" a string into an integer safely in Rust using `.parse().unwrap()`.

**Part 4: Cargo (The Modern Toolchain)**
1. Research how **Cargo** acts as a build system, package manager, and test runner all in one.
2. Compare this to C/C++ where you often have to manage `Makefile` or `CMake` files manually.
3. Discuss how having a standardized toolchain helps a community collaborate on open-source projects.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Steep Learning Curve. The Rust compiler is "Grumpy." It will reject code that would be perfectly valid in Python or JS. Be patient; the compiler is teaching you how to write better, safer code.
- **Gotcha 2:** String vs &str. Rust has multiple types for text (one on the heap, one as a fixed-slice). This is confusing for beginners but essential for performance.

### Reflection Question
Why are companies like Microsoft, Google, and Amazon moving their core infrastructure (Linux kernel, AWS firecracker) from C++ to Rust?
