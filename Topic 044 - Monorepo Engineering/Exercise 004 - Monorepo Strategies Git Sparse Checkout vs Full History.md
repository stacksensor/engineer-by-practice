# Exercise 004 - Monorepo Strategies: Git Sparse Checkout vs. Full History

### Objective
Scale the source. Learn how to manage the "Infinite Repo" size by using **Sparse Checkout** and **Shallow Clones**. Understand why a 50GB monorepo cannot be used like a 10MB microservice repo and how to download only the folders you need.

### Core Concepts to Master
- **Sparse Checkout:** A Git feature that allows you to "Opt-in" to only specific folders (e.g., `git sparse-checkout set apps/login`).
- **Shallow Clone (`--depth 1`):** Downloading only the *current* state of the code, ignoring 10 years of history to save disk space.
- **VFS for Git (Virtual File System):** How Microsoft (Windows repo) and Google manage repos so large that a normal `ls` command would take 1 minute.
- **Monorepo Bloat:** Why every "Large Binary" (Images, Videos) must be kept out of a monorepo (use LFS or S3).

### Research Topics
- "Git Sparse Checkout: How to use it in a monorepo"
- "Microsoft Scalar: Scaling Git for massive repositories"
- "Git LFS (Large File Storage) vs. Monorepo Performance"
- "Comparison of Google's Piper vs. GitHub for monorepos"

---

### The Practical Challenge

**Part 1: The "50GB Repo" Disaster (Scenario)**
1. You join a company with a 50GB monorepo.
2. You run `git clone`. It takes 4 hours.
3. **The fix:** 
   - Research the `git clone --filter=blob:none` command. 
   - Discuss: How does this "On-demand" downloading change the developer experience?
   - Answer: You only download the *metadata* first, and Git fetches the *content* only when you open a file.

**Part 2: The "Sparse" Setup**
1. You only work on the "Frontend" team.
2. In a monorepo, you have `/backend`, `/mobile`, `/data-science`, and `/frontend`.
3. Use the concept of **Sparse Checkout** to "Hide" everything except `/frontend` and `/shared-libs`.
4. Discuss: Does your IDE (VS Code) run faster if it only has to "Index" 1,000 files instead of 1,000,000? (Answer: Significantly).

**Part 3: The "LFS" Strategy**
1. Someone commits a 1GB video to the monorepo.
2. Now, 10,000 developers have to download that video.
3. Research **Git LFS**. 
4. Discuss: Why does LFS only store a "Pointer" in Git while the video stays on a separate server?
5. Answer: Because Git is a "History" tool, and changing a video creates a NEW 1GB copy in history forever.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Broken Links. If you "Sparse Checkout" only your folder, but your folder depends on a "Shared Utility" folder you didn't download, your code won't compile. (Solution: Always include `shared/*` in your sparse config).
- **Gotcha 2:** Deep History. Even a small repo can be 10GB if it has 50,000 commits. (Solution: Use `--depth 1` for CI builds to save time).

### Reflection Question
If your company repo grows to 100GB, why is "Sparse Checkout" no longer an option, but a mandatory requirement for every employee?
