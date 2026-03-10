# Exercise 007 - The Art of the Code Review (Senior Edition)

### Objective
Review for **Architecture**, not just **Syntax**. Master the "Senior" approach to code reviews. Move beyond "Nitpicking" (formatting, naming) to focus on the long-term impact of a change: its maintainability, performance, security, and how it fits into the broader system architecture. Learn how to use PRs as a tool for teaching and culture building.

### Core Concepts to Master
- **Review Levels:**
  - **Syntax/Style:** (Automated by Linters).
  - **Logic/Bugs:** Is the code correct?
  - **Architecture:** Does this change introduce a bad dependency? Does it scale?
  - **Culture:** Is the PR description clear? Are there tests?
- **LGTM (Looks Good To Me):** What it actually means to put your name on someone else's code.
- **Nitpicking vs. Blocking:** Distinguishing between "I would have named this `result`" (Nit) and "This will cause a memory leak" (Blocking).
- **The "Rubber Stamp" Problem:** Approving code without actually reading it (usually due to time pressure).

### Research Topics
- "Google's internal code review guidelines"
- "Phases of a Code Review: Architecture, Cleanliness, Bugs"
- "How to give kind but firm code reviews"
- "The cost of 'Over-reviewing' and 'Under-reviewing'"

---

### The Practical Challenge

**Part 1: The "Architectural" Review**
1. Imagine a PR that adds a new feature by importing a massive 20MB library that does 500 things the app doesn't need.
2. The code "Works" and has 100% test coverage.
3. Write a review comment explaining why this is an "Architectural Mistake" (Increase in bundle size, security risk of 3rd party code, long-term maintenance).

**Part 2: Separating "Style" from "Safety"**
1. Read a hypothetical code snippet.
2. Identify 3 "Nits" (e.g., "Missing a space after `if`").
3. Identify 1 "Showstopper" (e.g., "User input is being passed directly to an SQL query").
4. Practice writing the review: 
   - Prefix the nits with `Nit:` or `Non-blocking:`.
   - Make the showstopper very clear and offer a fix.

**Part 3: The "Reviewer's Responsibility"**
1. If you approve a PR and that PR causes a major production outage, is it "Your Fault"?
2. Discuss the concept of "Shared Ownership." 
3. Research the "Bus Factor" and how code reviews help increase the number of people who understand a piece of code.

**Part 4: Managing "Large" PRs**
1. You receive a PR with 2,000 lines of code changes and 50 files.
2. Discuss: Why is this PR impossible to review effectively?
3. Roleplay telling the engineer: "This is too big to review safely. Can we break this into 3 smaller, independent changes?".

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Endless Loop." If a PR has 50 comments and the conversation is going in circles, STOP typing. Get on a 5-minute Zoom call or meet in person to resolve the dispute.
- **Gotcha 2:** Ignoring the "Why." If you don't understand *why* a change was made, you cannot effectively review *how* it was done. Ask for a better PR description before starting.

### Reflection Question
How does a "Senior Code Review" act as a form of "On-the-job training" for everyone else on the team?
