# Exercise 001 - Monorepos: One Repo to Rule Them All

### Objective
Unify the codebase. Master the concept of **Monorepos**—the "Google-style" practice of putting all your company's code (Frontend, Backend, Mobile, Shared Libraries) into a single Git repository. Learn when to use this vs the "Many-Repos" (Polyrepo) approach and understand the trade-offs of scale.

### Core Concepts to Master
- **Monorepo:** A single repository containing many distinct projects and libraries.
- **Polyrepo:** Each project having its own separate repository.
- **Code Sharing:** Reusing a `utils` folder across 5 different apps smoothly.
- **The Dependency Problem:** If Project A updates a shared library, it might "Break" Project B without anyone knowing (in a Polyrepo).
- **Workspaces (Node/Rust/Go):** The built-in language feature for managing multiple projects in one folder.

### Research Topics
- "Monorepo vs Polyrepo: The ultimate comparison"
- "How Google manages its multi-gigabyte monorepo"
- "Microsoft, Meta, and Twitter: Monorepo users"
- "Code Sharing in a monorepo"

---

### The Practical Challenge

**Part 1: The "Polyrepo" Inefficiency**
1. You have 2 Repos: `Frontend` and `Backend`, and a shared library `Types-Lib`.
2. You change a type in `Types-Lib`.
3. Discuss the 3 steps to update both apps:
   - Commit and Push `Types-Lib`.
   - Update `package.json` in `Frontend` and `Backend`.
   - Build and test both.
4. Discuss: How long does this complex "Dancing" take every time you change a single line of code?

**Part 2: The "Monorepo" Speedup**
1. You move them all into one repo: `/apps/frontend`, `/apps/backend`, `/libs/types`.
2. You change the type. 
3. Discuss why you can now "Test" every app on your own machine in 1 second without pushing anything.

**Part 3: The "Scale" Problem**
1. Research what happens to a Monorepo when it reaches **1,000,000 lines of code**. 
2. Discuss why `git clone` or `npm install` might take 30 minutes. 
3. (Answer: This is why you need "Sparse Checkout" and specialized monorepo tools).

**Part 4: Identifying the tool for the job**
1. Research these monorepo-friendly languages:
   - **Go:** (Works with `go.work`).
   - **Node.js:** (Works with `npm workspaces` or `pnpm workspaces`).
   - **Rust:** (Works with `Cargo Workspaces`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Tight Coupling. Because it's "Too easy" to share code, you might accidentally make your "Order Service" depend on your "Frontend UI Components" (Bad!).
- **Gotcha 2:** CI Pipeline Explosion. If you have 50 apps in 1 repo, and your CI runs ALL 50 on every pull request, your "Build Time" will become 5 hours. (Note: Search for "Affected Builds" to fix this).

### Reflection Question
Why is a Monorepo considered a "Culture" choice rather than a "Technical" choice? (Answer: Because it forces every team to be responsible for keeping the whole company's code working).
