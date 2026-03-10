# Exercise 002 - Dependency Managers: NPM, Pip & Cargo

### Objective
Lock the version. Master **Dependency Managers**—the tools that find, download, and manage the 3rd-party code (Libraries) your app needs to run. Learn how to use `npm`, `pip`, or `cargo` to install a package and understand why the **Lockfile** (`package-lock.json`) is the most important file in your repository.

### Core Concepts to Master
- **Package Manager:** The tool (e.g., `npm`, `yarn`, `pip`, `cargo`, `gem`).
- **The Registry:** The "Store" where code is kept (e.g., `npm.js`, `pypi.org`, `crates.io`).
- **Semantic Versioning (SemVer):** `Major.Minor.Patch` (e.g., `1.2.3`).
- **The Manifest File:** `package.json` or `requirements.txt`. (The list of things you WANT).
- **The Lockfile:** `package-lock.json` or `poetry.lock`. (The list of EXACT things you HAVE).

### Research Topics
- "SemVer explained: Major vs Minor vs Patch"
- "Why you should never delete your package-lock.json"
- "NPM vs Yarn vs PNPM: A comparison"
- "The concept of 'Transitive' dependencies"

---

### The Practical Challenge

**Part 1: The "Version" Tilde vs Caret**
1. Research the difference in `package.json`:
   - `"lodash": "^4.17.0"` (Caret) 
   - `"lodash": "~4.17.0"` (Tilde)
2. Discuss: If a library releases `4.17.5`, which one will install it? If they release `4.18.0`, which one will install it? 
3. (Answer: Caret allows `4.18.0`; Tilde only allows `4.17.X`).

**Part 2: The "Lockfile" Surprise**
1. You have `lodash: "^4.0.0"` in your `package.json`.
2. Developer A runs `npm install` on Monday (gets version `4.1.0`).
3. Developer B runs `npm install` on Friday (gets version `4.5.0` because it was released that morning).
4. Discuss: If `4.5.0` has a bug, why is Developer B's app broken while Developer A's app works? 
5. How does the **Lockfile** solve this? (Answer: Everyone gets the exact same version regardless of when they run the command).

**Part 3: The "Scrub" (Cleanup)**
1. Research the **`node_modules`** or **`target/`** folder. 
2. Discuss why these folders are 1,000x larger than your source code. 
3. (Answer: They contain the source code of every library you use, and every library *they* use). 
4. Why should they ALWAYS be in your `.gitignore`? (Answer: Because they are "Generated" files, not "Source" files).

**Part 4: Identifying the manager**
1. Which manager for:
   - "A Python data science script" (Answer: `pip` or `poetry`).
   - "A Rust performance tool" (Answer: `cargo`).
   - "A Ruby web server" (Answer: `bundler`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "It works on my machine!" This usually happens because your colleague has a different version of a library than you (Hidden in their global packages). Always use **Local Dependencies**.
- **Gotcha 2:** The "Supply Chain" attack. If a hacker takes over a popular library and releases version `2.0.1` with a virus, and you have `^2.0.0` in your manifest, you might install the virus automatically! (Solution: Audit your dependencies!).

### Reflection Question
Why is the "Dependency" part of a build system considered the most "Unstable" part? (Answer: Because you are trusting code you didn't write, stored on a server you don't control).
