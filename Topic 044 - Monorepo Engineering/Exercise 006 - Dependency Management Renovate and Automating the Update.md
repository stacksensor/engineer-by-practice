# Exercise 006 - Dependency Management: Renovate and Automating the Update

### Objective
Automate the maintenance. In a monorepo, keeping 100 packages up to date manually is impossible. Master **Renovate** or **Dependabot** to update 1,000 dependencies across your entire company with a single Pull Request.

### Core Concepts to Master
- **Renovate:** The "Advanced" bot that groups 20 updates (e.g., all `Next.js` sub-packages) into ONE branch to save CI time.
- **Grouping:** Why a monorepo should update `React` and `React-DOM` together to avoid "Version Hell."
- **Automerge:** If a "Minor" update (e.g., `Lodash 4.0.0` -> `4.0.1`) passes all 1,000 tests, why a human should NOT have to click the "Merge" button.
- **Dependency Pinning:** When it is SAFER to lock `Node v20` across the whole company than letting everyone pick their own version.

### Research Topics
- "Renovate Bot config for monorepos: `preset:monorepo`"
- "Grouped Dependabot updates in a single Pull Request"
- "Automerge best practices: Risk vs. Speed"
- "Policy-driven updates in a large organization"

---

### The Practical Challenge

**Part 1: The "1,000 PRs" Disaster (Scenario)**
1. You have a monorepo with 50 apps and 50 libs.
2. `Lodash` has a security bug. 
3. **The fix:** 
   - Research the Renovate **`groupName`** feature.
   - Discuss: Instead of creating 100 PRs (1 for each app), why would you create ONE PR for the whole monorepo?
   - Answer: Because you fix the security bug in the ROOT folder, and every app is protected instantly.

**Part 2: The "Automerge" Trust**
1. You have 95% test coverage in your monorepo.
2. A robotic update to a "Formatting" tool (e.g., `Prettier`) is created.
3. Why wait 24 hours for a human review?
4. Discuss the **Automerge** strategy.
5. Answer: If tests pass, the robot merges the code at 2 AM. 
6. Discussion: What happens when the tests *miss* a bug and the robot merges it? (Solution: **Rollback** scripts).

**Part 3: The "Version" Sync**
1. App 1 uses `Bootstrap 4`. App 2 uses `Bootstrap 5`.
2. A shared "Button" library is created in the monorepo.
3. Which Bootstrap version should the Button use? (Answer: It can't use both).
4. Discuss: How does a monorepo "Force" the company to stay modern by making it painful to stay on old versions?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** CI Overload. If your bot creates 50 PRs in 1 minute, your CI (GitHub Actions) bill will explode. (Solution: Use **Schedule** to only run the bot on Sundays).
- **Gotcha 2:** Merge Conflicts. If 2 bots try to update the same Lockfile, the second one will fail. (Solution: Use Renovate's **`platformAutomerge`**).

### Reflection Question
Why is a monorepo the "Antidote" to technical debt in large companies? (Answer: Because it makes it impossible to hide an 'Old Version' of a library in a corner of the company for 5 years).
