# Exercise 005 - Database Performance (Deep Dive)

### Objective
Unblock the query. Deepen your understanding of **Database Indexing** and **Query Execution Plans**. Learn how to identify when a database is doing a "Full Table Scan" (Reading every single row on disk) vs an "Index Seek" (Efficiently jumping to the result). Understand how to "Explain" your SQL in **Postgres** or **MySQL**.

### Core Concepts to Master
- **The B-Tree Index:** The "Phonebook" of your database.
- **Full Table Scan (Sequential Scan):** Reading 1,000,000 rows because you forgot to index a column. (Slow!).
- **Index Seek (Index Scan):** Going straight to the row using the B-Tree. (Fast!).
- **EXPLAIN (ANALYZE):** The SQL command that reveals the "Execution Plan" and actual time spent in each step.
- **The Covering Index:** An index that contains ALL the data your query needs (no need to even look at the "Main Table").
- **Cost Approximation:** How the DB "Guesses" if an index will be faster than a scan.

### Research Topics
- "How B-Tree indexes work: Under the hood"
- "Reading a Postgres EXPLAIN ANALYZE output"
- "Why adding TOO many indexes makes 'Writes' (INSERT/UPDATE) slower"
- "The concept of 'Composite' (Multi-column) indexes"

---

### The Practical Challenge

**Part 1: The "Search" Pain**
1. You have a table with 1,000,000 Users.
2. Query: `SELECT * FROM users WHERE email='alex@gmail.com'`.
3. If there is NO index on `email`, how many disk reads does the DB have to do? (Answer: 1,000,000 - the entire file).
4. If there IS an index, how many reads? (Answer: ~10 to 20 - the height of the B-Tree).
5. Discuss: Why does this make your search 50,000x faster?

**Part 2: The EXPLAIN (Conceptual)**
1. In Postgres: `EXPLAIN ANALYZE SELECT * FROM users WHERE id=5;`.
2. Look for keywords:
   - **`Seq Scan`**: (Answer: Bad! Red alert!).
   - **`Index Scan`**: (Answer: Good! Green light!).
   - **`Actual time`**: (The true latency).
3. Try this in a local DB (or online SQL playground) and watch the time change when you add an index.

**Part 3: The Multi-Column Puzzle**
1. You have an index on `(first_name, last_name)`.
2. Query A: `WHERE first_name='Alex'`. (Answer: Uses index).
3. Query B: `WHERE last_name='Smith'`. (Answer: **DOES NOT USE INDEX!**).
4. Discuss: Why does the "Order" of columns in a composite index matter? 
5. (Hint: Think of a phonebook sorted by Lastname-Firstname. Can you find all "Alex's" easily? No!).

**Part 4: Identifying the optimization**
1. Research **N+1 Query** problem. 
2. Discuss why sending 100 small queries to a database is 100x slower than sending 1 large "JOIN" query.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Outdated Statistics. If you delete 90% of your data, the database might still "Think" it needs a Full Scan because its internal statistics are old. Run `ANALYZE` (Postgres) or `OPTIMIZE` (MySQL).
- **Gotcha 2:** High Write overhead. Every time you `INSERT`, the DB must update ALL your indexes. If you have 20 indexes on one table, every write becomes extremely slow.

### Reflection Question
Why is the "Execution Plan" of a database query considered its "Intelligence," and why does it sometimes choose to "Scan" even if an index is available? (Answer: Cost estimation - for small tables, scanning the whole thing in RAM is faster than navigating a B-Tree).
