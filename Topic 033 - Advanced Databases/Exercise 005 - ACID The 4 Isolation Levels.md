# Exercise 005 - ACID & The 4 Isolation Levels

### Objective
Define the rules of engagement. Master the **ACID** properties (Atomicity, Consistency, Isolation, Durability) and understand the **4 Isolation Levels** (Read Uncommitted, Read Committed, Repeatable Read, Serializable). Learn how to choose the right level to balance **Performance** and **Correctness**.

### Core Concepts to Master
- **Atomicity:** "All or nothing." If one part of a transaction fails, everything fails.
- **Consistency:** The database moves from one valid state to another valid state (no broken rules).
- **Isolation:** Transactions don't step on each other's toes.
- **Durability:** Once committed, the data is safe even if the power goes out.

- **The 4 Isolation Levels:**
  1. **Read Uncommitted:** Can see "dirty" (uncommitted) data from others.
  2. **Read Committed:** Only sees committed data (Default for Postgres/SQL Server).
  3. **Repeatable Read:** Guarantees that if you read a row twice, it won't change.
  4. **Serializable:** The strictest level. Acts as if transactions happened one-by-one.

### Research Topics
- "The ACID properties explained"
- "Dirty Reads, Non-repeatable Reads, and Phantom Reads"
- "Postgres default isolation level"
- "When to use Serializable isolation?"

---

### The Practical Challenge

**Part 1: Identifying the Anomaly**
1. Research the **"Phantom Read"**. 
2. Imagine you count the users (Result: 10). Someone else inserts a new user and commits. You count again (Result: 11).
3. Which isolation level would prevent this? (Answer: Serializable).

**Part 2: The Default Check**
1. Check the isolation level of your current DB: `SHOW TRANSACTION ISOLATION LEVEL;` (Postgres). 
2. Discuss why "Read Committed" is the most common default (balance between speed and safety).

**Part 3: The Durability Promise**
1. Research how a database ensures **Durability** (Hint: **Write-Ahead Log**). 
2. Discuss: If the database "Commits" but hasn't written the data to the main table yet when the power dies, how does it recover?

**Part 4: The Performance Penalty**
1. Discuss why "Serializable" is the slowest level. 
2. (Answer: Because the database has to track every single row you've looked at and potentially "Abort" other transactions if they try to touch those rows).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Assuming "Repeatable Read" solves everything. In some databases, Repeatable Read still allows "Phantoms."
- **Gotcha 2:** The "Serialization failure." If you use Serializable isolation, your application code MUST be prepared to "Retry" transactions that are aborted by the database due to conflicts.

### Reflection Question
Why is the "I" (Isolation) in ACID the most difficult and expensive property to maintain in a globally distributed system?
