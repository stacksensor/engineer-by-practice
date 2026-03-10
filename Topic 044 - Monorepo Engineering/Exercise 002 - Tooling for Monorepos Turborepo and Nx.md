# Exercise 002 - Monorepo Tools: Turborepo & Nx

### Objective
Visualize the dependency. Master **Monorepo Tooling**—the specialized software that makes managing 50 apps in 1 repo feel as easy as 1 app. Learn about **Turborepo** and **Nx**, understand the concept of a **Task Graph**, and learn how to run a "Build" that only touches the projects you actually changed.

### Core Concepts to Master
- **The Task Graph:** A diagram showing which app depends on which library. (e.g., `App A` -> `UI-Lib`, `App B` -> `Auth-Lib`).
- **Turborepo:** The fast, lightweight build tool for JavaScript/TypeScript monorepos. (Easy to setup).
- **Nx:** The "Full-featured" toolkit for monorepo development (includes code generation, testing, and more).
- **The "Affected" Command:** Running only the tests for the code you JUST modified. (e.g., `nx affected:test`).
- **Parallel Execution:** Running the "Build" for 5 apps at the SAME time on different CPU cores.

### Research Topics
- "Turborepo vs Nx: Which one is right for my team?"
- "Building a 'Task Graph' in Nx/Turborepo"
- "How to run 'Affected' builds in a Monorepo"
- "The concept of 'Remote Caching' for monorepos (Vercel/Nx Cloud)"

---

### The Practical Challenge

**Part 1: The "100-App" Build (Scenario)**
1. You have 100 Javascript Apps. 
2. Without a tool like **Turborepo**, you run a `for` loop: 
   - `for app in apps: cd $app && npm run build`.
3. Total Time: 30 minutes.
4. Using **Turborepo Parallel**: All 100 apps build in parallel. 
5. Total Time: 3 minutes. (Time of the slowest single app).
6. Discuss: How much time did you save? (Answer: 27 minutes!).

**Part 2: The "Affected" Logic (Concept)**
1. You change one CSS file in `Shared-Library-A`.
2. `App 1` uses `Shared-Library-A`.
3. `App 2` uses `Shared-Library-B`.
4. Discuss: If you use an **Affected Build**, does `App 2` rebuild? 
5. (Answer: No! The tool knows `App 2` doesn't care about `Library-A`).

**Part 3: The Task Graph (Visual)**
1. Research the command: `nx graph` (or `npx turbo --graph`).
2. Draw a simple graph:
   - `Store-App` -> `Payment-Lib` -> `Core-Logging-Lib`.
   - `User-App` -> `Auth-Lib` -> `Core-Logging-Lib`.
3. Discuss: If you change `Core-Logging-Lib`, why must you test the WHOLE company's code? (Answer: Because it's the foundation of everything!).

**Part 4: Identifying the tool**
1. Research **Nx**. 
2. Discuss why "Code Generation" (e.g., `nx generate app my-new-app`) is better than manually creating folders and files. 
3. (Answer: It ensures every app in the company follows the same "Standards").

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Phantom" Dependencies. If `App 1` imports code from `App 2` (instead of a shared library), your task graph will become a "Spider Web" and your builds will become slow. (Solution: Never import from another 'App' folder).
- **Gotcha 2:** The "Version" bottleneck. If you use a tool like **Nx**, you must use the EXACT same version of React/Typescript across all 100 apps. This is a "Policy" you must follow!

### Reflection Question
Why is a "Task Graph" considered the "Map" of a company's architecture in a monorepo? (Answer: Because it reveals how interconnected your services really are, showing you which libraries 'Break' the most apps when they change).
