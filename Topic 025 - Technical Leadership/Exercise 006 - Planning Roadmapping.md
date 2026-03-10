# Exercise 006 - Planning & Roadmapping

### Objective
Define the "North Star." Learn how to translate high-level business goals into a multi-month **Engineering Roadmap**. Master the art of **Estimation** (at scale), understand the trade-offs of "Build vs Buy," and learn how to plan for "Technical Refactors" alongside "Product Features."

### Core Concepts to Master
- **The Engineering Strategy:** A document describing how the engineering team will evolve to support the business over the next 1-2 years.
- **T-Shirt Sizing:** Using broad categories (Small, Medium, Large) for long-term planning instead of precise hours.
- **The "Build vs Buy" Matrix:** Deciding when to build a custom solution vs when to pay for a SaaS (e.g., "Build our own auth" vs "Buy Auth0").
- **Roadmap Balancing:** Allocating a % of every month to "Stability/Infrastructure" vs "Product Growth."
- **Dependencies:** Identifying when Project A cannot start until Project B is finished.

### Research Topics
- "How to build an engineering roadmap"
- "Engineering strategy vs Tactics"
- "The 70-20-10 rule for engineering work allocation"

---

### The Practical Challenge

**Part 1: The Build vs. Buy Decision**
1. Roleplay: Your company needs a new "Product Indexing Service."
2. **Option A (Build):** 3 engineers, 4 months of work, full control, $0 monthly cost.
3. **Option B (Buy):** 1 engineer, 1 week of integration, $5,000 / month, limited customization.
4. Discuss the "Opportunity Cost": If you *build* this, what *other* feature are you NOT building during those 4 months?

**Part 2: Planning the "Migration"**
1. Your app has 50 microservices and you want to move them all from "Direct VM" to "Kubernetes."
2. Break this down into 3 Phases:
   - Phase 1: Foundation (Networking, Registry).
   - Phase 2: The "Pilot" (Move the 2 smallest services).
   - Phase 3: The "Migration" (Move the rest over 6 months).
3. Discuss why "Doing it all at once" is a recipe for disaster.

**Part 3: The Roadmap Balancing Act**
1. You have 10 developers. 
2. The Product Manager wants 10 New Features. The CTO wants a "Database Upgrade." The Team wants to fix 50 "Small Bugs."
3. Design a "Capacity Plan" (e.g., 6 developers on Features, 2 on Database, 2 on Bugs/On-call). 
4. Defend this plan to the Product Manager.

**Part 4: Managing "Scope Creep"**
1. Research what occurs when "Small features" slowly grow into "Massive Projects."
2. Discuss the importance of a "Frozen" Roadmap vs an "Agile" Roadmap.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Optimism" Bias. Engineers almost always underestimate how long a project will take. Always add a "Buffer" (usually 1.5x to 2x) for unexpected incidents, sick leave, and technical hurdles.
- **Gotcha 2:** The "Shadow" Roadmap. If developers are secretly working on a "New framework" because they are bored, while the official roadmap is falling behind, the team has a trust problem.

### Reflection Question
Why is a Roadmap a "Communication Tool" more than it is a "Truth"?
