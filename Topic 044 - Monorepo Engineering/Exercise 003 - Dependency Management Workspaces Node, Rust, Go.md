# Exercise 003 - Monorepo Dependencies: Workspaces

### Objective
Share the library. Master **Workspaces**—the built-in feature of modern languages (Node, Rust, Go) for managing multiple sub-projects in a single folder. Learn how to configure `package.json` (NPM), `Cargo.toml` (Rust), or `go.work` (Go) to recognize and link your internal "Library" to your "App" without using the internet.

### Core Concepts to Master
- **Workspaces:** A setting in your "Root" config file that lists all your sub-folders. (e.g., `workspaces: ["apps/*", "libs/*"]`).
- **Internal Aliasing:** Importing `import { log } from "@my-lib/logger"` even if the logger is in a folder on your same disk.
- **The "One Version" Rule:** Making sure every app in the monorepo uses `React v18.0.0` to avoid "Library Conflicts" in your shared code.
- **Dependency Hoisting:** Putting all your `node_modules` in the root folder so you only have ONE copy of `Express` for 10 apps. (Saves GBs of RAM and Disk).
- **The Root lockfile:** One single `package-lock.json` for the whole company.

### Research Topics
- "NPM Workspaces vs Yarn Workspaces: Setting up a monorepo"
- "Introduction to Go Workspaces (go.work)"
- "Managing multiple crates in a Rust Cargo Workspace"
- "Hoisting in Node.js Workspaces (and how to disable it)"

---

### The Practical Challenge

**Part 1: The "Local" Link (Scenario)**
1. You have a folder `/apps/web` and `/libs/utils`.
2. In a standard project, to use `utils` in `web`, you must publish `utils` to the internet (NPM). (Wait 5 minutes).
3. Using **Workspaces**, you add `libs/utils` to your `package.json`. 
4. Link it instantly: `import { helper } from "../../libs/utils"`.
5. Discuss: Why does this feel like "One giant app" instead of two separate ones?

**Part 2: The "Hoisting" Math**
1. 10 Apps each use `React` (10MB).
2. **Without Workspaces:** Total `node_modules` = 100MB.
3. **With Workspaces:** Only 1 copy of `React` in `/node_modules`. Total = 10MB.
4. Discuss: If you have 50 dependencies, how much disk space do you save across 100 developers? (Answer: Gigabytes!).

**Part 3: The "Go" Workspaces (Concept)**
1. Research **`go.work`**. 
2. Discuss why it was invented specifically to help developers who work on "Two separate repos" at the same time locally.

**Part 4: Identifying the config**
1. Which file for:
   - "A Rust Monorepo" (Answer: `Cargo.toml` with `[workspace]` block).
   - "A Node.js Monorepo" (Answer: `package.json` with `workspaces` field).
   - "A Go Monorepo" (Answer: `go.work`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Ghost" Dependencies. If `App A` accidentally uses a library that only `App B` has installed (because of hoisting), your code will work on your laptop but crash in CI. (Solution: Use **pnpm workspaces** which prevent this).
- **Gotcha 2:** Version Mismatch. If `App 1` uses `Lodash 4.0` and `App 2` uses `Lodash 3.0`, hoisting will fail and you will have "Two version hell." (Solution: Always keep versions identical in a monorepo).

### Reflection Question
Why are "Workspaces" the #1 technical requirement for building a monorepo? (Answer: Because they allow you to 'link' internal projects together without needing an external Registry).
