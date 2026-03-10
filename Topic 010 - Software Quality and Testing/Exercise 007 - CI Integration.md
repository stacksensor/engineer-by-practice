# Exercise 007 - CI Integration (GitHub Actions)

### Objective
Automate the execution of test suites on centralized repository servers. Ensure no broken unit test reaches the main branch. Learn YAML configuration for GitHub Actions pipelines.

### Core Concepts to Master
- **Continuous Integration (CI):** Automating software builds and testing whenever a developer pushes a code commit.
- **Continuous Deployment (CD):** Pushing verified, pre-tested code to live production servers.
- **Matrix Builds:** Running testing logic against multiple unique versions of Node.js concurrently.
- **Workflow State Checks:** GitHub rules that block pull request merges if the associated CI script fails.

### Research Topics
- "Basic GitHub Actions workflow setup"
- "YAML language syntax crash course"
- "Running npm tests via GitHub actions"

---

### The Practical Challenge

**Part 1: The Remote Repository Setup**
1. Initialize a Git repository containing the Node.js project from Exercise 002.
2. Commit your code.
3. Push the branch to a public GitHub repository.
4. Verify the `npm test` script runs locally without syntax errors. Ensure all dependencies are in your `package.json`.

**Part 2: The Action Configuration**
1. In the root directory of your project, create the `.github/workflows/` folder.
2. Inside that folder, create a YAML file named `build.yml`.
3. Define the trigger for the workflow (e.g., when a push happens to the `main` branch):
   ```yaml
   name: Node.js CI
   on:
     push:
       branches: [ main ]
   ```

**Part 3: The Build Process**
1. Configure the runner environment in your YAML file. Use `ubuntu-latest`.
2. Define the steps to clone the code and setup the Node.js environment:
   ```yaml
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
         - name: Setup Node
           uses: actions/setup-node@v3
           with:
             node-version: 18.x
   ```

**Part 4: Executing the Suite**
1. Add commands to install dependencies and run tests:
   ```yaml
         - run: npm ci
         - run: npm test
   ```
2. Commit the `build.yml` file and push it to GitHub.
3. Navigate to the "Actions" tab in your GitHub repository and watch the cloud server execute your test suite.
4. Intentionally cause a test failure in your code and push the change to verify that the GitHub Action correctly flags the failure.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Using `npm install` instead of `npm ci`. In a CI environment, `npm ci` is preferred because it uses the `package-lock.json` file to install exact versions of dependencies, ensuring a stable and reproducible environment.
- **Gotcha 2:** Ignoring `node_modules` in your repository. Ensure you have a `.gitignore` file that excludes the `node_modules` folder, as committing it will make your repository bloated and potentially cause architecture-specific failures on the CI server.

### Reflection Question
Why do continuous integration scripts typically use `npm ci` instead of `npm install` for dependency management?