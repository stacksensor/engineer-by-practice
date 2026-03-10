# Exercise 007 - Incremental Builds & Caching: Turborepo Strategy

### Objective
Build 10x faster with 10x more code. Master **Incremental Builds**—the art of "Reading" your previous build and only rebuilding what actually changed. Learn about **Turborepo**, **Bazel**, and **Nx** for Monorepos and understand the concept of "Remote Caching" where one developer's build is shared with everyone else.

### Core Concepts to Master
- **Incremental Build:** "Only rebuild the modules that changed." (If you change the CSS, don't re-compile the 1,000,000 lines of Java code).
- **The Task Graph:** A visual map of which project depends on which. (e.g., `App A` depends on `Lib B`. If `Lib B` changes, rebuild both).
- **Content-based Hashing:** Using a "Hash" of the file contents (e.g., `xyz-123`) to see if anything changed.
- **Local Cache:** Saving the results in a local `.turbo` or `.cache` folder. 
- **Remote Cache:** Saving the results in the "Cloud" (Vercel, AWS S3, etc.). If Developer A builds `Lib B`, Developer B "Downloads" the binary instantly without building it!

### Research Topics
- "Turborepo vs Nx: A comparison of monorepo build tools"
- "Bazel: The high-speed build system from Google"
- "What is 'Hermetic' build? (No side effects)"
- "Using 'Remote Caching' in a CI/CD pipeline"

---

### The Practical Challenge

**Part 1: The "100-App" Build (Scenario)**
1. You have 100 Javascript Apps and 50 Shared Libraries in one **Monorepo**.
2. **Standard Build:** 30 minutes (Runs every app one by one).
3. **Incremental Build:** If you change **App 1**, it only builds App 1. Time: 1 minute.
4. Discuss: How much time did you save? (Answer: 29 minutes per push!).

**Part 2: The "Remote" Surprise**
1. Developer A builds the `Auth-Library` on their laptop.
2. Developer B pulls the latest code and runs `npm run build`. 
3. Observe: The terminal says **`>>> FULL TURBO (Cache Hit)`** and finishes in 0.1s.
4. Discuss: Why did Developer B not have to "Wait" for the build? 
5. (Answer: They "Pulled" the binary that Developer A already uploaded to the remote cache).

**Part 3: The Task Graph (Concept)**
1. Research the **Task Graph** in **Turborepo** or **Nx**.
2. Build a simple graph: `Web` depends on `API`, which depends on `Shared-Types`.
3. If you change `Shared-Types`, which ones must rebuild? (Answer: All of them).
4. If you change `Web`, do you need to rebuild `API`? (Answer: No!).

**Part 4: Identifying the "Input"**
1. Research the **`inputs`** setting in a build tool. 
2. Discuss why "Ignoring" the `README.md` from the build hash is essential. (Answer: So the build doesn't restart just because you fix a typo in the documentation!).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Corrupt Cache. Sometimes the cache gets "Stuck" (e.g., a file was deleted but the cache doesn't know). (Solution: Run `rm -rf .turbo` or `npm run build -- --force`).
- **Gotcha 2:** High Complexity. Tools like **Bazel** are extremely powerful but also extremely hard to learn. Don't use them for a "Small" project! Use them only when your build takes more than 10 minutes.

### Reflection Question
Why are "Incremental Builds" the only way to manage a "Monorepo" with millions of lines of code? (Answer: Because a 'Complete' build of a company like Google or Facebook would take weeks to run on a single machine).
