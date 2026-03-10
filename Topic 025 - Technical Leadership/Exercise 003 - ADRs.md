# Exercise 003 - ADRs (Architecture Decision Records)

### Objective
Capture the "Why," not just the "How." Learn how to use **ADR (Architecture Decision Records)** to document the significant technical decisions made during the life of a project. Ensure that when a new engineer joins in 2 years, they can understand exactly why a specific database or framework was chosen.

### Core Concepts to Master
- **ADR:** A short text file (usually in Markdown) that captures a single decision.
- **Components of an ADR:**
  - **Context:** The situation we were in when the decision was made.
  - **Decision:** What we decided to do.
  - **Status:** (Proposed, Accepted, Superceded, Deprecated).
  - **Consequences:** The positive and negative effects of this decision in the future.
- **The "Living" Repository:** Storing ADRs directly in the codebase (e.g., in a `/docs/adr` folder).

### Research Topics
- "What is an ADR (Architecture Decision Record)?"
- "Michael Nygard: Documenting Architecture Decisions"
- "ADR vs RFC: When to use which?"
- "ADR templates and tools (`adr-tools`)"

---

### The Practical Challenge

**Part 1: Identifying a Decision**
1. Review a project you are working on. 
2. Identify a "Significant Decision" (e.g., "We chose Python instead of Rust," or "We are using JWTs for auth instead of Sessions").
3. Discuss: Why is this considered an "Architectural Decision" and not just a "Coding Detail"?

**Part 2: Writing the Record**
1. Create a file `0001-use-postgres-for-inventory.md`.
2. Fill in the **Context**: "We are launching a new inventory system that requires strict ACID compliance and complex relational queries."
3. Fill in the **Consequences**:
   - Positive: "We can use JSONB for flexible fields."
   - Negative: "We need to manage database migrations and scaling."

**Part 3: The "Superceded" Flow**
1. Imagine 2 years pass. The team decides to move from Postgres to a specialized Graph database.
2. Do NOT delete the original ADR. 
3. Create a new ADR: `0045-move-to-neo4j.md`.
4. Update the status of ADR #0001 to `Superceded by ADR #0045`.
5. Discuss why keeping the "History" is more valuable than having a "Clean" doc folder.

**Part 4: The ADR Audit**
1. Research how to integrate ADRs into the PR process. 
2. Discuss: Every time a PR makes a major change in direction, the reviewer should ask "Where is the ADR for this?".

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-documenting. You don't need an ADR for "We chose a 2-space indentation." Focus on things that would be expensive or difficult to change later.
- **Gotcha 2:** The "Invisible" Doc. If the ADRs are in a separate Wiki or Google Drive, engineers will never read them. Keep them in the Git repository.

### Reflection Question
How does reading old ADRs help a new Staff Engineer understand the "Technical Culture" of a company?
