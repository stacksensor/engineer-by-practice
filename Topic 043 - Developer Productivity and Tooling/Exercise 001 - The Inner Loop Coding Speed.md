# Exercise 001 - The Inner Loop: Coding Speed

### Objective
Minimize the friction. Master the **Inner Loop**—the "Code-Save-Build-Test" cycle that every developer performs 100 times a day. Learn how to optimize this cycle using **Auto-Reload**, **Fast Unit Tests**, and **Instant Feedback** so you can stay in "The Flow" and write better code faster.

### Core Concepts to Master
- **The Inner Loop:** The speed of the `Save -> See Change` cycle. (In React: HMR; In Go/Rust: Fast incremental build).
- **HMR (Hot Module Replacement):** Updating the CSS/JS in the browser without refreshing the whole page.
- **Auto-Test (Watch Mode):** Automatically running your unit tests every time you save a file. (E.g., `npm test -- --watch`).
- **Linting & Formatting:** Using `ESLint` or `Prettier` to fix errors *as you type* so you don't waste time on typos.
- **Context Switching:** The "Cost" of checking Slack while your code builds for 1 minute.

### Research Topics
- "What is the Developer 'Inner Loop'?"
- "Optimizing your local development environment"
- "Vite vs Webpack: HMR speed comparison"
- "Using 'Watch' tools for non-web projects (e.g., `nodemon` or `entr`)"

---

### The Practical Challenge

**Part 1: The "Manual" Pain**
1. Write a small script to print "Hello." 
2. Change it to say "Bye." 
3. Manually run the command to see the change. 
4. Repeat 5 times. 
5. Discuss: How much attention is "lost" during those few seconds of switching windows?

**Part 2: The "Watch" Solution**
1. Use a tool like **`nodemon`** (Node) or **`entr`** (Shell).
2. Configure it to run your script every time the file is saved.
3. Discuss: Why does this feel more like "Play" and less like "Work"?

**Part 3: The Fast Test**
1. Research the **`--watch`** flag in your favorite test runner (e.g., `jest`, `pytest`, `vitest`).
2. Observe how the tests "Turn Green" instantly as you fix a bug.

**Part 4: Identifying the blocker**
1. Research the "Build Time" of a massive project like the **Linux Kernel** or **Chromium**. 
2. Discuss: If a build takes 2 hours, can those developers have an "Inner Loop"? (Answer: No, they have to use "Partial Builds" or "Remote Build Farms").

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** False Positives in Auto-Reload. Sometimes the "Old" state of the app sticks around in the browser's memory, causing a bug that would be "Fixed" if you just did a hard refresh.
- **Gotcha 2:** Ignoring the Linter. If your IDE is full of "Squiggly Red Lines," don't ignore them! Fixing them at the source is 10x faster than finding them later in a CI pipeline.

### Reflection Question
Why are the "Top 1%" of productive developers often the ones who spend the most time "Optimizing their tools"? (Answer: Because saving 5 seconds every minute adds up to years of saved time over a career).
