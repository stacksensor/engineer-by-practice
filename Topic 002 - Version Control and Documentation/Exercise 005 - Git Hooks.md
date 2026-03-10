# Exercise 005 - Git Hooks & Technical Automation

### Objective
Automate quality control at the source. Implement Git Hooks to automatically run linters, tests, or formatters before code is even allowed to be committed, ensuring your repository remains clean and stable without manual intervention.

### Core Concepts to Master
- **Git Hooks:** Scripts that Git executes automatically when specific events happen (e.g., `pre-commit`, `pre-push`, `post-merge`).
- **Client-side vs Server-side Hooks:** Understanding that hooks live in the `.git/hooks` folder and are not normally shared via `git clone`.
- **Husky & lint-staged:** Modern JavaScript tools used to manage and share Git hooks across a development team easily.
- **Exit Codes in Hooks:** Learning that a non-zero exit code in a `pre-commit` hook will physically prevent the commit from finishing.

### Research Topics
- "What are git hooks and how to use them"
- "Setting up Husky for React projects"
- "Preventing commits if tests fail using git hooks"
- "Git hooks directory structure"

---

### The Practical Challenge

**Part 1: Manual Hook Creation**
1. Navigate to `.git/hooks` in your project.
2. Notice the `.sample` files. Create a new file named `pre-commit` (no extension).
3. Add a simple script: 
   ```bash
   #!/bin/bash
   echo "Running pre-commit check..."
   exit 1
   ```
4. Make it executable: `chmod +x .git/hooks/pre-commit`.
5. Try to commit a file. Git should block you and show your message. This is the "Gatekeeper" in action.

**Part 2: Automated Linting**
1. Update your hook to run a real command (e.g., `npm run lint` or `eslint .`).
2. Fix the script so it only exits with `1` if the linting command fails.
3. Intentionally add a syntax error to a file and try to commit. Watch as Git refuses to accept the bad code.

**Part 3: Shared Hooks with Husky**
1. Discuss the problem: Your teammates don't have your manual hook.
2. Install Husky: `npx husky-init && npm install`.
3. Observe the new `.husky` directory. This directory *is* committed to Git, allowing all developers to share the same rules.
4. Configure a `pre-push` hook that runs your unit test suite.

**Part 4: Advanced Formatting**
1. Combine Husky with `lint-staged`.
2. Configure it so that only the files you are currently committing are "Auto-formatted" by Prettier before the commit finishes.
3. This ensures that every piece of code in your repo follows exactly the same style guide perfectly.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The `--no-verify` escape hatch. If you are in a rush and need to bypass your hooks, you can run `git commit -m "msg" --no-verify`. Use this sparingly, as it bypasses all safety checks.
- **Gotcha 2:** Hook permissions. On Mac/Linux, hooks *must* be executable. On Windows, this is handled differently, often requiring tools like Husky to bridge the gap.

### Reflection Question
Why are shared Git hooks (via Husky) considered a vital "First Line of Defense" for large software engineering teams?
