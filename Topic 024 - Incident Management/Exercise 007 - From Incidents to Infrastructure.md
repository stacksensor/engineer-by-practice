# Exercise 007 - From Incidents to Infrastructure

### Objective
Complete the feedback loop. Learn how to transform the "Pain" of an incident into the "Roadmap" for your future architecture. Master **Reliability Engineering** by using incident data to justify technical debt removal, infrastructure upgrades, and "Chaos Engineering" experiments.

### Core Concepts to Master
- **Reliability Backlog:** A dedicated list of engineering tasks derived specifically from Post-Mortems.
- **Error Budgets:** Using your "Up-time" data to decide when to focus on Features vs. when to focus on Stability.
- **Chaos Engineering:** Intentionally breaking things in a controlled environment (Game Days) to see if your incident response works.
- **Architectural Guardrails:** Using the lessons of the past to build "Safety by Design" (e.g., if one database was slow, moving to a Multi-AZ cluster).

### Research Topics
- "What is Chaos Engineering? (Principles of Chaos)"
- "Using error budgets to balance speed and stability"
- "Running a Game Day with your team"

---

### The Practical Challenge

**Part 1: The "Game Day"**
1. Design a "Controlled Failure" exercise for your team.
2. Objective: "What happens if our Main API goes down?"
3. Plan the test: Run it in the **Staging** environment. Turn off the service.
4. Record the outcome:
   - Did the alerts fire? 
   - How long did it take to find the runbook?
   - Did the fallback search work?

**Part 2: Prioritizing Technical Debt**
1. You have 10 "Follow-up Actions" from an incident. 
2. Use a "Cost vs. Benefit" matrix to decide which ones to do first.
3. (Benefit: Reduced risk of another $100k outage. Cost: 2 weeks of developer time).

**Part 3: The Error Budget Policy**
1. If your Service Level Objective (SLO) is 99.9% uptime, you are allowed 43 minutes of downtime per month.
2. If you use up 40 minutes in the first week because of buggy code, discuss the "Shipping Freeze" policy where the team stops all new features to work purely on stability for the rest of the month.

**Part 4: Predictive Architecture**
1. Review the last 3 incidents in your repository (or hypothetical ones).
2. Look for patterns: "Is it always the database?", "Is it always a Friday deployment?".
3. Propose one major infrastructure change that would eliminate that specific *category* of incident forever (e.g., "Implementing Canary Deploys").

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-Correcting. Don't build a $1 million redundant backup system for a bug that cost $5. Balance the solution with the actual risk.
- **Gotcha 2:** Chaos without Control. Never run "Chaos Engineering" in production until you have successfully survived it multiple times in Staging.

### Reflection Question
How do incidents act as the "Best Teacher" for a Senior Software Engineer?
