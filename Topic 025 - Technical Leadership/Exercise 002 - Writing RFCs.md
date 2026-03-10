# Exercise 002 - Writing RFCs (Request for Comments)

### Objective
Design in the light. Master the process of writing an **RFC (Request for Comments)**. Learn how to document a complex technical proposal—including its goals, proposed implementation, and trade-offs—to gather feedback from other engineers *before* you start writing code.

### Core Concepts to Master
- **RFC:** A document used to propose a new feature, a change in architecture, or a new standard.
- **The Lifecycle:** Writing -> Initial Feedback -> Wide Review -> Approval/Rejection -> Implementation.
- **Problem Statement:** Clearly defining "Why" we are doing this. What is the pain we are solving?
- **Alternative Solutions:** Listing the other ways we *could* have solved the problem and why we rejected them.
- **Consensus Building:** Using the document to move the team toward a shared agreement.

### Research Topics
- "What is an RFC in software engineering?"
- "The Uber/Facebook/Google RFC process"
- "RFC templates for engineering teams"

---

### The Practical Challenge

**Part 1: The Problem Definition**
1. Imagine your team has 5 different ways of writing logs, making it impossible to debug.
2. Write a "Problem Statement" for an RFC titled: "Standardizing Logging across Microservices."
3. (Hint: Focus on the *business impact*, e.g., "It takes us 2 hours to find an error because logs are inconsistent").

**Part 2: The Proposed Solution**
1. Document the plan: "We will use the `pino` library and every log must include a `correlation_id` and `timestamp`."
2. Write a section on "Backward Compatibility." How will we handle the 100 existing services that don't follow this rule?

**Part 3: The "Alternatives Considered"**
1. List 2 other options:
   - Option A: "Do nothing" (The cost of maintenance).
   - Option B: "Use the `winston` library."
2. Explain why your chosen solution (Pino) is better (e.g., performance, easier to learn).

**Part 4: Handling Feedback**
1. Imagine an engineer comments: "I hate this library, I want to use my own custom logger instead."
2. Practice a "Staff Engineer" response that is professional, open to feedback, but firm on the goal of standardization.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Writing a 50-page Book. Nobody will read a massive, bloated RFC. Keep it concise. Focus on the decisions that matter.
- **Gotcha 2:** Only asking your friends. An RFC is only useful if it is seen by people who might *disagree* with you. Seek out the "Naysayers" early.

### Reflection Question
How does writing an RFC help prevent "Redoing the work" when you get halfway through a project and realize your architecture is fundamentally flawed?
