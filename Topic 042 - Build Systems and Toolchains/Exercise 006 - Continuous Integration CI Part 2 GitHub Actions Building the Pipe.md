# Exercise 006 - CI Part 2: GitHub Actions (The Pipeline)

### Objective
Automate the build. Master **GitHub Actions**—the tool that automatically "Builds, Tests, and Deploys" your code every time you `git push`. Learn how to define a **Workflow** (using YAML), configure **Jobs** and **Steps**, and understand why "Automation" is the only way to ship code 10 times a day without breaking everything.

### Core Concepts to Master
- **Workflow:** The ".github/workflows/main.yml" file. (The recipe).
- **Trigger (Event):** `on: push` or `on: pull_request`. (When the action starts).
- **Runner:** The "Virtual Machine" (Ubuntu/Mac/Windows) on GitHub's servers that runs your code.
- **Job:** A set of steps (e.g., 'Test' job).
- **Step:** A single action (e.g., `npm install`).
- **Secrets:** Safely storing your `STRIPE_KEY` in GitHub's "Actions Secrets" so the YAML file can use it without revealing it to the public.

### Research Topics
- "GitHub Actions: Core concepts (Events, Jobs, Steps)"
- "Writing your first simple 'Hello World' GitHub Action"
- "Passing 'Artifacts' (files) between separate GitHub jobs"
- "Using 'Matrix' builds to test on 5 versions of Node.js at once"

---

### The Practical Challenge

**Part 1: The "Manual" Forget (Scenario)**
1. You have 2 Developers. 
2. Alex runs `npm test` before pushing to `main`. 
3. Bob forgets to run `npm test` and pushes a bug.
4. **Main is now broken!**
5. Discuss: How does a **GitHub Action** that runs `npm test` for EVERY push fix this "Human" mistake? 
6. (Answer: The "Merge" button turns red if the test fails).

**Part 2: The YAML Definition (Concept)**
1. Write a snippet: 
   - `on: push`
   - `jobs: test-app:`
   - `runs-on: ubuntu-latest`
   - `steps: - uses: actions/checkout@v4`
   - ` - run: npm install`
   - ` - run: npm test`
2. Discuss: Why does "ubuntu-latest" matter? 
3. (Answer: Because it ensures your code runs on a "Clean" machine, not just your laptop).

**Part 3: The Secret Injection**
1. You need an `API_KEY` to deploy. 
2. Research **`secrets.API_KEY`** in GitHub Actions. 
3. Discuss: If you put the key in your code, anyone can see it. If you put it in GitHub's "Secrets" vault, only the "Action" runner can see it.

**Part 4: Identifying the "Matrix"**
1. Research the **`strategy: matrix`** command. 
2. Discuss: Why is it 10x faster to test on MacOS and Linux at the SAME time instead of one after another?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Infinite Loop." If your Action "Pushes" to Git, and your Trigger is "on: push," your Action will trigger itself forever! (Solution: Use `[skip ci]` in your commit message).
- **Gotcha 2:** Cost. GitHub Actions aren't "Free" for private repos once you use up your monthly minutes. If your tests take 30 minutes to run, you will pay $$$! (Solution: Use "Caching" for `node_modules`).

### Reflection Question
Why is "CI/CD" considered the "Nerve System" of a modern software company? (Answer: Because without it, you can't trust the code you are about to merge).
