# Exercise 004 - Compilers & Transpilers: Babel & SWC

### Objective
Change the language. Master the two most common "Language Changers": **Compilers** (Source-to-Binary) and **Transpilers** (Source-to-Source). Learn how **Babel** and **SWC** allowed the web to use modern Javascript even if browsers didn't support it yet, and understand why the "Speed" of your compiler is the #1 factor in your developer productivity.

### Core Concepts to Master
- **Compiler:** e.g., `rustc`, `gcc`, `go build`. Turns text into a binary.
- **Transpiler (Source-to-Source Compiler):** e.g., `Babel`, `TypeScript (tsc)`. Turns modern Javascript into "Old" Javascript for old browsers. (e.g., `let` converts to `var`).
- **Babel:** The flexible, plugin-based transpiler for the web. (Slow).
- **SWC / esbuild:** The new, high-speed transpilers written in Rust/Go. (100x faster than Babel).
- **Minification:** Scrambling your code (removing spaces, shortening variable names: `count` -> `a`) to make the file smaller. (Part of the build chain).
- **Polyfill:** A small "Library" that adds missing features (like `fetch` or `Promise`) to old browsers. (A "Simulation" of the new language).

### Research Topics
- "The difference between Compiling and Transpiling"
- "How Babel works: Parser, Transformer, Generator"
- "SWC vs Babel: A performance comparison"
- "What is a 'JavaScript engine' (like V8) and how does it execute your code?"

---

### The Practical Challenge

**Part 1: The "Modern" to "Old" (Transpiling)**
1. You write: `const name = "Alex"; console.log(<code>Hi ${name}</code>);`.
2. Look at the "Babel output" for Internet Explorer 11:
   - `"var name = 'Alex'; console.log('Hi ' + name);"`.
3. Discuss: Why is it important to support users who can't upgrade their browsers? 
4. How does a transpiler make this "Automatic" for you?

**Part 2: The "Speed" Test (SWC)**
1. A project has 1,000 files. 
2. **Babel (JS):** Takes 10 seconds to build.
3. **SWC (Rust):** Takes 0.1 seconds to build.
4. Discuss: How much more "Coding" can you do in a day if your build is 100x faster? 
5. (Answer: Thousands of extra 'Save-and-See' attempts).

**Part 3: The "Map" (Source Maps)**
1. Research **Source Maps**. 
2. Discuss why they are essential for "Debugging." 
3. (Answer: Without them, when your app crashes, the browser will say the error is on "Line 1, Column 50,000" of your scrambled minified file. A source map tells the browser: "That's actually Line 10 of `App.js`!").

**Part 4: Identifying the "Chain"**
1. Research the **TypeScript** Compiler (`tsc`). 
2. Discuss why "Type Checking" is part of the build step: (Answer: To catch bugs *before* the code ever hits the computer).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Supporting "Too many" browsers. If you support IE6, your transpiled file will be 10x larger and slow for everyone. Use a **Browserslist** file to only support the "Last 2 versions" of modern browsers.
- **Gotcha 2:** The "Transpile-on-the-fly" slow-down. If you run your server with `ts-node` (which transpiles every file when it's requested), your production app will be extremely slow. Always "Pre-build" into plain Javascript for production!

### Reflection Question
Why are new build tools (like Vite and SWC) moving away from Javascript and being "Rewritten in Go/Rust"? (Answer: For raw performance - compiling text is a CPU-heavy task, and Go/Rust are 10-100x faster than NodeJS for this).
