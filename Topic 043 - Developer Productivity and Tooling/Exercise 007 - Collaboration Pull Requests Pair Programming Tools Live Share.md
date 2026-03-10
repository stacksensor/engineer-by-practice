# Exercise 007 - Collaboration: Pull Requests & Pair Programming

### Objective
Work with the team. Master **Developer Collaboration**—the tools and practices for writing code together. Learn how to use **Pull Requests (PRs)** (GitHub/GitLab) to review each other's code, understand the value of **Pair Programming** (VS Code Live Share), and learn how to write a "Readable" commit message so your team doesn't hate you.

### Core Concepts to Master
- **The Pull Request (PR):** A request to "Merge" your code into the main project. (Where 'Code Review' happens).
- **Code Review:** Your teammate looks at your code and gives feedback (e.g., 'Is there a faster way to do this?').
- **Pair Programming:** 2 Developers, 1 Screen. (Fastest way to learn and solve bugs).
- **VS Code Live Share:** A tool that allows you to "Invite" a friend to your IDE while you code.
- **Commit Messages:** Writing `fix: handle null user` instead of `asdf`. (The "Conventional Commits" standard).

### Research Topics
- "How to write a good Pull Request description"
- "The 4 Rules of Pair Programming"
- "Using 'VS Code Live Share' for remote pairing"
- "Conventional Commits: A standard for Git messages"

---

### The Practical Challenge

**Part 1: The "Invisible" Team (Scenario)**
1. You work on a feature for 1 week.
2. You push 50 files at once.
3. Your teammate Alex must "Review" them.
4. Discuss: How much attention can Alex pay to 50 files? 
5. (Answer: Very little! You will likely have many bugs).
6. How does a **Small PR** of 2-3 files fix this? (Answer: Alex can actually read every line).

**Part 2: The "Pairing" Experiment**
1. Research **VS Code Live Share**. 
2. Discuss how it feels to have someone else's "Cursor" in your file. 
3. Why is this better than "Sharing your screen" on Zoom? 
4. (Answer: Your friend can actually Scroll, Type, and Debug in their own editor!).

**Part 3: The "Readable" Git History**
1. Imagine 10 developers all using `fixed` as their commit message.
2. 6 months later, you want to find why the "Login" logic changed.
3. Discuss: How long does it take by looking at the logs? 
4. If they used `feat(auth): login with Google`, how long would it take? (Answer: 2 seconds!).

**Part 4: Identifying the "Rule"**
1. Research the **"Don't be a Jerk"** rule in Code Reviews. 
2. Discuss why writing "This code is stupid" is worse than writing "Can we try a different approach for this loop?" 
3. (Answer: Collaboration is all about trust and communication).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The PR "Holding Pattern." If your team takes 3 days to review a PR, your "Velocity" will be zero. (Solution: Set an "SLO" for code reviews - e.g., 'Reviews finished in < 4 hours').
- **Gotcha 2:** Only pairing. If you pair 100% of the time, you might never learn to solve problems by yourself. Balance is key!

### Reflection Question
Why is "Communication" considered the most important "Tool" in a developer's productivity toolbox, even more than their computer? (Answer: Because software engineering is a 'Team Sport,' and one person working alone will almost always fail to build a large product).
