# Exercise 001 - Query Planners & The "EXPLAIN" Command

### Objective
See inside the brain of the database. Master the **Query Planner** (or Optimizer). Learn how the database decides which index to use, whether to perform a "Scan" or a "Seek," and how to use the **EXPLAIN** command to diagnose why a specific SQL query is running slowly.

### Core Concepts to Master
- **The Planner:** The component that transforms a SQL string into a "Plan" (a series of steps like "Scan table X", "Filter by Y").
- **Sequential Scan:** Reading every single row in the table (Slow for large tables).
- **Index Scan/Seek:** Using a map to jump directly to the right rows (Fast).
- **Statistics:** The "Data about the data" (e.g., how many users are in the US) that the planner uses to make decisions.
- **Cost Estimation:** How the database "scores" different plans to find the cheapest one.

### Research Topics
- "How the Postgres Query Planner works"
- "Reading EXPLAIN ANALYZE output"
- "Sequential Scan vs Index Scan"
- "Why did the database ignore my index?"

---

### The Practical Challenge

**Part 1: The "Simple" Explain**
1. Using a local Postgres installation (or any SQL DB).
2. Create a table `users` with 10,000 rows. Do NOT add an index yet.
3. Run: `EXPLAIN SELECT * FROM users WHERE email = 'test@example.com';`.
4. Observe the output. Identify the words **"Seq Scan"**. 
5. What is the reported "Cost"? 

**Part 2: The Index Speedup**
1. Add an index: `CREATE INDEX idx_email ON users(email);`.
2. Run the `EXPLAIN` again.
3. Observe the output changing to **"Index Scan"** or **"Index Seek"**.
4. Compare the "Cost" and the "Execution Time."

**Part 3: EXPLAIN ANALYZE**
1. Research the difference between `EXPLAIN` (a guess) and `EXPLAIN ANALYZE` (actually running the query and measuring).
2. Run a query that returns 0 rows. 
3. Observe the difference between the "Estimated rows" (Guess) and "Actual rows" (Truth).
4. Discuss: Why would the guess be wrong? (Answer: Outdated statistics).

**Part 4: Identifying "Hidden" Scans**
1. Run a query that uses an unindexed column in the `WHERE` clause alongside an indexed one.
2. Observe how the database might still decide to do a "Sequential Scan" if it believes the filter isn't selective enough.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Table size. The planner is smart. If your table has only 10 rows, it will ignore your index and do a sequential scan because "Reading the whole table" is faster than "Looking at a map then reading the data."
- **Gotcha 2:** Functions on columns. If you query `WHERE UPPER(email) = '...'`, the database will ignore your index on `email`. You need a "Functional Index" for this to work.

### Reflection Question
Why is the Query Planner considered the most complex and secretive part of a database engine? (Answer: Because its cost-estimation math determines the performance of every single enterprise application).
