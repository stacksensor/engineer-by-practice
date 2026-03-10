# Exercise 006 - WebAssembly (Wasm) Integration

### Objective
Break the JavaScript performance barrier. Learn how to compile high-performance code written in C++, Rust, or C into the WebAssembly (Wasm) format to execute CPU-intensive tasks (like image processing or physics simulations) at near-native speeds inside the browser.

### Core Concepts to Master
- **WebAssembly (Wasm):** A binary instruction format that provides a way to run high-performance languages on the web alongside JavaScript.
- **The Sandbox:** How Wasm executes within the same security boundaries as JavaScript, with no direct access to the DOM.
- **Emscripten / Rust-wasm:** The compilers used to transform C/C++ or Rust code into `.wasm` modules.
- **Interoperability:** Passing data (numbers, strings, and arrays) between the JavaScript "Main Thread" and the Wasm execution module.

### Research Topics
- "What is WebAssembly and how does it work?"
- "Compiling Rust to WebAssembly with wasm-pack"
- "When to use WebAssembly vs JavaScript"
- "WebAssembly vs Web Workers"

---

### The Practical Challenge

**Part 1: The Hello-Wasm Module**
1. Use an online compiler (like WasmFiddle) or follow a basic Rust `wasm-pack` tutorial to generate a simple `.wasm` file.
2. The module should export a function called `add(a, b)` that performs a simple addition in a compiled language.
3. In your JavaScript code, use the `WebAssembly.instantiateStreaming` API to load the binary file.
4. Execute the `add` function from JS and log the result to the console.

**Part 2: The Performance Bench**
1. Create a "Fibonacci" function in both JavaScript and your chosen Wasm language (e.g., Rust).
2. Calculate the 45th Fibonacci number using both implementations.
3. Use `performance.now()` to measure the execution time of both.
4. Observe the speed difference. Compiled code typically excels at recursive, mathematical operations that strain the JS JIT (Just-In-Time) compiler.

**Part 3: Memory & Pointers**
1. Wasm cannot "read" JavaScript memory directly. It has its own `Linear Memory` (a large array of bytes).
2. Allocate a buffer in JavaScript, fill it with data (e.g., pixels from a canvas), and pass the "Pointer" (index) to the Wasm module.
3. Have the Wasm module perform a heavy operation (like a Blur or Grayscale filter) directly on the shared memory buffer.
4. Read the resulting data back in JavaScript and update the UI.

**Part 4: Real-world Integration**
1. Search for a pre-compiled Wasm library (e.g., `ffmpeg.wasm` or `sqlite-wasm`). 
2. Integrate a small feature from one of these libraries into a web project.
3. Discuss how WebAssembly allows developers to bring existing "C++ desktop software" to the browser without rewriting it in JavaScript.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Communication Overhead. While Wasm code is fast, "sending" large amounts of data back and forth between JS and Wasm can be slow. It is often faster to do a task in slow JS than to send it to Wasm if the operation is small.
- **Gotcha 2:** No DOM Access. Wasm cannot `document.getElementById()`. All UI updates must still be handled by JavaScript after Wasm finishes its calculations.

### Reflection Question
Why is WebAssembly considered a "Companion" to JavaScript rather than a "Replacement"?
