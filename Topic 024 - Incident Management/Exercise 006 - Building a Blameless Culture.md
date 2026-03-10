# Exercise 006 - Building a "Blameless" Culture

### Objective
Foster psychological safety. Learn why "Blame" is the enemy of reliability. Understand the **Blameless Culture**—a philosophy popularized by Etsy and Google—where the focus is on fixing the *system* rather than punishing the *individual*. Learn how to build a team where engineers feel safe reporting their mistakes immediately.

### Core Concepts to Master
- **The Attribution Bias:** The tendency to blame a person's character ("He was lazy/careless") rather than the situation ("The UI was confusing").
- **Psychological Safety:** The belief that one will not be punished or humiliated for making a mistake or speaking up.
- **Systemic Failures:** The realization that most "Human Errors" are actually the result of bad tools, poor documentation, or missing guardrails.
- **Reporting Culture:** Success is measured by how quickly people admit they broke something, not by how few things break.

### Research Topics
- "Etsy's Guide to Blameless Postmortems"
- "The concept of Psychological Safety in high-performing teams"
- "John Allspaw: Fault vs Blame"

---

### The Practical Challenge

**Part 1: The "Blame" Script**
1. Read this Slack message: "Who deployed this buggy code? You just cost the company $50,000. Be more careful next time!"
2. Discuss: If you are the engineer who made the mistake, will you be *more* or *less* likely to admit it quickly next time?
3. Rewrite this message to be **Blameless**. (Hint: Focus on the *process* that allowed the bug to get into production).

**Part 2: The "Just Culture" (Conceptual)**
1. Research the difference between "Honest Mistakes" and "Gross Negligence."
2. Discuss: Does "Blameless" mean "Zero Accountability"? (Answer: No. It means we hold the system accountable first).
3. If a pilot crashes a plane because the controls were confusing, we fix the controls. If a pilot crashes because they were drunk, we fire the pilot. Identify that line in software engineering.

**Part 3: Roleplay: The Post-Mortem Meeting**
1. Imagine you are leading a meeting about a major outage.
2. An executive asks: "Whose fault was it?"
3. Practice your response: "The system allowed an unvalidated change to go live. We are here to fix the system, not point fingers at the person who typed the command."

**Part 4: Rewarding Honesty**
1. Research **"The Three-Armed Sweater"** award (or similar concepts).
2. Discuss why some companies publicly "Thanks" the person who breaks the site if they also help fix it and document the learning.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Passive-Aggressive Blame. Even if you don't say a name, phrases like "It's obvious that SOMEONE didn't read the docs" is still blame.
- **Gotcha 2:** Only at the Top. A blameless culture must be supported by the CEO and VPs. If the engineers are blameless but the CEO fires the Manager after an outage, the culture is dead.

### Reflection Question
How does "Blaming an engineer" actually make your system *more* dangerous over time? (Hint: Think about what people start hiding).
