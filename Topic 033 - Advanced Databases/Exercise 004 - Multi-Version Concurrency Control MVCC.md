# Exercise 004 - Multi-Version Concurrency Control (MVCC)

### Objective
Read while someone else writes. Master the magic of **MVCC (Multi-Version Concurrency Control)**—the reason you can read from a table without being "Blocked" by a long-running update. Understand how the database keeps multiple "Versions" of the same row simultaneously to provide a consistent "Snapshot" of the data to every user.

### Core Concepts to Master
- **The Snapshot:** Every transaction sees a "Frozen" version of the database as it existed when the transaction started.
- **xmin & xmax:** Identifying row visibility based on the ID of the transaction that created or deleted it.
- **Non-blocking Reads:** Why "Readers never block Writers, and Writers never block Readers" in modern databases.
- **The "Vacuum" / Garbage Collection:** Cleaning up the "Dead" versions of rows that are no longer needed by any active transaction.

### Research Topics
- "How Postgres MVCC works"
- "xmin, xmax, and cmin columns in Postgres"
- "Transaction isolation and snapshots"
- "What is 'Bloat' in a database?"

---

### The Practical Challenge

**Part 1: The Invisible Update**
1. Open two database terminals (Terminal A and Terminal B).
2. Terminal A: `BEGIN; UPDATE users SET age = 22 WHERE id = 1;`. (Do NOT commit).
3. Terminal B: `SELECT age FROM users WHERE id = 1;`.
4. Observe that Terminal B still sees the **Old** age.
5. Discuss: Why does Terminal B NOT see "22" yet? Why is it not "Waiting" for Terminal A to finish?

**Part 2: The Dirty Secret (xmin/xmax)**
1. In Postgres, run: `SELECT xmin, xmax, * FROM users;`.
2. Observe the transaction IDs.
3. Update a row and check again. Observe how the `xmin` has changed.
4. Discuss: How does the database know that a row is "Dead" and can be deleted by the Vacuum?

**Part 3: The "Bloat" Experiment**
1. Research what happens if you have a "Long-running transaction" that stays open for 24 hours.
2. Discuss: Why does this prevent the "Vacuum" from cleaning up ANY rows, even ones that the long transaction isn't using? 
3. (Answer: The database must keep every version that *could* have been visible to that transaction).

**Part 4: Conflict Identification**
1. Discuss the "Write-Write" conflict: If A and B both try to update the SAME row at the same time, what does MVCC do? (Answer: The second one must wait for the first one to Commit or Rollback).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Deadlock by long transactions. If you forget to `COMMIT` in a script, you might accidentally block maintenance tasks (like VACUUM or INDEX REBUILD) for the entire table.
- **Gotcha 2:** Storage Overhead. Because every update creates a "New copy" of the row, an update-heavy workload can grow the disk size of the database by 2x-5x compared to the actual data size.

### Reflection Question
How does MVCC solve the "Phantoms and Dirty Reads" problem without using heavy table-level locks? (Answer: By giving every transaction its own private view of the data).
