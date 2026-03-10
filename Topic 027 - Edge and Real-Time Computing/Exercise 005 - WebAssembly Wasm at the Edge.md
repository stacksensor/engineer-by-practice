# Exercise 005 - WebAssembly (Wasm) at the Edge

### Objective
Native speed in the sandbox. Learn how to use **WebAssembly (Wasm)** to run high-performance code (written in Rust, C++, or Go) on the edge. Understand how Wasm allows you to perform complex tasks like image processing, cryptography, or heavy mathematical calculations at "Native" speeds that were previously impossible in JavaScript.

### Core Concepts to Master
- **WebAssembly (Wasm):** A binary instruction format for a stack-based virtual machine, designed as a portable compilation target for high-level languages.
- **Isolates + Wasm:** How platforms like Cloudflare use V8 to execute Wasm modules with near-zero overhead.
- **Memory Safety:** Why Wasm is more secure than traditional "Native Binaries" because it runs inside a sandboxed environment.
- **Portability:** Writing a library once in Rust and running it in the Browser, on the Server, and at the Edge.

### Research Topics
- "What is WebAssembly and why use it at the edge?"
- "Compiling Rust to WebAssembly (wasm-pack)"
- "Image processing at the edge with Wasm"

---

### The Practical Challenge

**Part 1: The Rust-to-Wasm Flow**
1. Install Rust and `wasm-pack`.
2. Create a simple Rust library with a function `calculate_pi(iterations: u32) -> f64`.
3. Compile it to Wasm: `wasm-pack build --target web`.

**Part 2: Edge Integration**
1. Create a Cloudflare Worker project.
2. Import your compiled `.wasm` module. 
3. Research the `WebAssembly.instantiate()` API or how Wasm is natively imported in your framework.
4. Write a script that takes a number from a query parameter and returns the result of the Rust function.

**Part 3: The Performance Bench**
1. Write a pure JavaScript version of the same `calculate_pi` function.
2. Run both versions 10,000 times inside the edge worker.
3. Measure the execution time. Notice the significant speedup with Wasm for this CPU-bound task.

**Part 4: Use Cases (Conceptual)**
1. Discuss 3 tasks that are "Bad" for JavaScript but "Great" for Wasm at the edge:
   - Resizing user-uploaded images on the fly.
   - Parsing massive JSON or Protocol Buffer files.
   - Real-time video frame manipulation (e.g., adding a watermark).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Bridge" overhead. Moving data between the JavaScript world and the Wasm world (the "Glue Code") can be slow. If your task is very simple, the overhead of moving the data might be greater than the speed gain of the Wasm execution.
- **Gotcha 2:** Standard Library missing. When you compile Rust/Go to Wasm, you don't have access to the full operating system (no `fs`, no direct network sockets). You must use the "Edge API" provided by the host.

### Reflection Question
How does WebAssembly solve the "Language Lock-in" problem for Edge platforms that traditionally only supported JavaScript?
