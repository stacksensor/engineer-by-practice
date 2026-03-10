# Exercise 007 - GitHub Actions & Automation

### Objective
Integrate your workflow into the cloud. Use GitHub Actions to automate CI/CD pipelines, allowing you to automatically run tests, build projects, and deploy code whenever you push to a specific branch.

### Core Concepts to Master
- **Workflows:** YAML files located in `.github/workflows` that define the automation steps.
- **Events:** Triggers that start a workflow (e.g., `push`, `pull_request`, `workflow_dispatch`).
- **Jobs & Steps:** The hierarchical structure of an automation pipeline.
- **Runners:** The virtual machines provided by GitHub that physically execute your scripts.

### Research Topics
- "GitHub Actions tutorial for beginners"
- "Understanding YAML syntax for GitHub Actions"
- "GitHub Actions vs Travis CI vs Jenkins"
- "Using GitHub Actions secrets for API keys"

---

### The Practical Challenge

**Part 1: The First Workflow**
1. In your GitHub repository, create the directory structure `.github/workflows`.
2. Create a file named `hello-world.yml`.
3. Add a basic workflow that prints "Hello from GitHub Actions" on every push.
4. Push the change and check the "Actions" tab on GitHub to see the successful run.

**Part 2: Automated Testing CI**
1. Create a `ci.yml` file.
2. Define a job that:
   - Sets up a specific Node.js or Python version.
   - Installs dependencies (`npm install`).
   - Runs your test suite (`npm test`).
3. Push a failing test and watch the GitHub UI turn "Red". Then fix it and watch it turn "Green".

**Part 3: Caching & Optimization**
1. Notice that `npm install` takes a long time on every run.
2. Research the `actions/cache` action.
3. Update your workflow to cache your `node_modules` or library folders, reducing build times by 50%+.

**Part 4: Deployment & Secrets**
1. Create a mock "Deployment" step.
2. Use GitHub "Secrets" to store a fake `DEPLOY_TOKEN`.
3. Update your workflow to echo "Deploying with token..." (but never echo the actual secret value!).
4. Discuss how this automation ensures that only "Green" (passing) code is ever deployed to production.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** YAML Syntax. Indentation is critical. If your `jobs` block is indented incorrectly, the workflow will fail to parse and won't show up in the Actions tab.
- **Gotcha 2:** Usage Limits. GitHub provides a generous free tier for Actions, but if you have a workflow that runs for 5 hours on every push, you will quickly run out of monthly credits.

### Reflection Question
How does moving automation from local Git Hooks (Exercise 005) to cloud-based GitHub Actions improve the reliability of a shared software project?
