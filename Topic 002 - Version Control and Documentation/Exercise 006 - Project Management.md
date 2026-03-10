# Exercise 006 - Project Management with Git (Issues & Projects)

### Objective
Organize your engineering workflow. Move beyond code to master the "Project Management" features of platforms like GitHub, using Issues, Labels, Milestones, and Kanban boards to track features, bugs, and progress.

### Core Concepts to Master
- **GitHub Issues:** Tracking bugs, enhancements, and tasks as distinct, commentable threads.
- **Labels & Milestones:** Categorizing issues (e.g., `bug`, `high priority`) and grouping them by release dates.
- **Pull Request Linking:** Automatically closing issues by using "magic" keywords (e.g., `Closes #5`) in your commit messages or PR descriptions.
- **GitHub Projects (Kanban):** Visualizing the workflow states: `Todo`, `In Progress`, `Review`, `Done`.

### Research Topics
- "How to use GitHub Issues effectively"
- "GitHub Project boards tutorial"
- "Linking pull requests to issues"
- "Issue templates for GitHub"

---

### The Practical Challenge

**Part 1: Defining the Tasks**
1. Create a new GitHub repository for a mock project.
2. Create 5 distinct "Issues" representing features you want to build (e.g., "Add Login Page", "Fix typo in Footer").
3. Assign "Labels" to each issue. Use colors to denote priority.

**Part 2: The Project Board**
1. Go to the "Projects" tab in GitHub.
2. Create a new "Table" or "Board" project.
3. Add your existing issues to the "Todo" column.
4. Drag one issue to "In Progress" to simulate that you are working on it.

**Part 3: Resolving with Code**
1. Create a local branch to fix one of your issues.
2. In your commit message, include the phrase `Fixes #1` (where 1 is your issue number).
3. Create a Pull Request. Observe how GitHub shows that merging this PR will automatically resolve the issue.
4. Merge the PR and verify the issue is closed.

**Part 4: Issue Templates**
1. Large projects need standardized reports.
2. Create a `.github/ISSUE_TEMPLATE` folder in your repo.
3. Add a `bug_report.md` file that asks the user for "Steps to Replicate" and "Expected Behavior."
4. Try to create a new issue. Observe how GitHub now gives the user a professional form to fill out.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Notification Fatigue. If you have 100 open issues and every comment sends an email, you will stop reading them. Learn to use "Subscriptions" and "Watch" settings to only see what matters.
- **Gotcha 2:** Stale Issues. Projects often have "Zombie Issues" from three years ago. Use a 'stale' bot or periodic "Triage" sessions to close what is no longer relevant.

### Reflection Question
How does using a visual Kanban board (Projects) improve a team's efficiency compared to just keeping a list of tasks in a text file?
