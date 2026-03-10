# Exercise 007 - Monorepo Lab: Building the "Mini-Google" Repository

### Objective
Integrate the system. Create a "Root" project that links an **App (Frontend)** and a **Lib (Backend)** together using **Workspaces** and **Turborepo** to build them in 1 second.

### Core Concepts to Master
- **The "Internal" Registry:** No more `npm publish` for your own company code.
- **The "Single CI" Pipeline:** Writing one `main.yml` that tests everything in one go.
- **The "One-Link" Editor:** Command-clicking a function in your App takes you to the *source code* of your Library instantly.
- **The "Infinite Scale" Mindset:** Why a monorepo is the choice for Facebook, Google, and Uber—the biggest tech companies in history.

### Research Topics
- "Turborepo vs NX: The final comparison in 2024"
- "Building a monorepo in 10 minutes with NPM Workspaces"
- "Running a monorepo with 100 developers: Performance tuning"
- "Why Google chose a monorepo (The scale story)"

---

### The Practical Challenge

**Part 1: The "Workspace" Root**
1. Create a `/root` folder.
2. Inside, add `/apps/web` and `/libs/utils`.
3. In `root/package.json`, add: `"workspaces": ["apps/**", "libs/**"]`.
4. Run **`npm install`** in the root. 
5. Discuss: Why are there no `node_modules` in the `apps` or `libs` folder? (Answer: Because they are all "Hoisted" to the root).

**Part 2: The "Link" test**
1. Inside `libs/utils`, create `index.ts` with `export const add = (a, b) => a + b`.
2. Inside `apps/web/package.json`, add `"dependencies": { "utils": "*" }`.
3. Now, import it in `apps/web/main.ts`: `import { add } from "utils"`.
4. Discuss: You didn't publish `utils` to the internet. How does the Web app find the "add" function?
5. Answer: Because the Workspace created a **Symlink** (a shortcut) between the two folders on your disk.

**Part 3: The "Infinite" Build**
1. Add **Turborepo** (`turbo.json`) to the root.
2. Define a `"build"` task. 
3. Run `npm run build`. It takes 10 seconds.
4. Run it AGAIN. It takes 0.1 seconds (**FULL CACHE**).
5. Discuss: If you only changed 1 file in the "Web" app, why did Turbo skip building the "Utils" library?
6. Answer: Because the "Hash" (the fingerprint) of the Utils folder didn't change, so Turbo used the "Video" of the old build instead of building it again.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Local caching. If one developer has a "Cached" build on their Mac that is broken, how do they fix it? (Solution: `rm -rf .turbo`).
- **Gotcha 2:** Remote caching. If your teammate build it on *their* computer, why should *you* have to build it? (Solution: Use **Vercel Remote Cache** to share build files across the internet).

### Reflection Question
If a monorepo is "Slower" for 2 developers, why is it "Faster" for 2,000 developers? (Answer: Because 'Redundant Work'—re-building or re-testing things that haven't changed—is eliminated at scale).
