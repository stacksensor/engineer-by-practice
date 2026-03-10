# Exercise 002 - Index Internals Part 1: B-Trees (Read-Optimized)

### Objective
Understand the backbone of SQL. Master the **B-Tree (Balanced Tree)** data structure. Learn how it keeps data sorted and allows for `O(log n)` search, insertion, and deletion. Understand why B-Trees are the default index for almost all RDBMSs (Postgres, MySQL, SQL Server) and why they are optimized for "Read-heavy" workloads.

### Core Concepts to Master
- **The B-Tree:** A self-balancing tree data structure that maintains sorted data.
- **Node Size:** Why B-Trees use "Wide/Flat" nodes (matching disk block sizes) rather than "Tall/Skinny" nodes (like binary trees).
- **Fan-out:** The number of pointers in each node. Higher fan-out means a shorter tree.
- **Search Complexity:** Jumping through a 1,000,000-row table in just 3-4 "Hops."
- **Range Queries:** Why B-Trees are amazing for `WHERE age > 18 AND age < 30`.

### Research Topics
- "How B-Trees work in databases"
- "Difference between a Binary Search Tree and a B-Tree"
- "B-Tree vs B+ Tree: The leaf node link"
- "Visualizing a B-Tree insertion"

---

### The Practical Challenge

**Part 1: The Binary Tree vs B-Tree Battle**
1. Draw a binary tree with 15 nodes. Note its height (4).
2. Draw a B-Tree (Fan-out 4) with the same 15 nodes. Note its height (2).
3. Discuss: If every "Height level" requires a slow disk read, which tree is faster?

**Part 2: The Search Path**
1. Imagine a B-Tree with 3 levels. 
2. Trace the search for the value `55`:
   - Root node: `[20, 50, 80]`. (Go to the child between 50 and 80).
   - Child node: `[55, 60, 70]`. (Found it!).
3. Discuss how the "Sorted" nature of the nodes allows for fast binary search within each node.

**Part 3: The Range Scan**
1. Research how **B+ Trees** link the leaf nodes together in a chain. 
2. Discuss why this makes "Find all users name starting with A" much faster than a standard tree search.

**Part 4: The Index Maintenance Cost**
1. Discuss: If you have 10 indexes on a table, what happens to the speed of your `INSERT` statements? 
2. (Answer: They get slower because the database has to update 10 different trees for every new row).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "High Cardinality" rule. Indexes are great for `email` (unique) but terrible for `gender` (only 2-3 values). If 50% of the table matches your query, the index is useless.
- **Gotcha 2:** Fragmentation. As you delete and update rows, the B-Tree nodes can become partially empty. This is why you sometimes need to "REINDEX" or "REORGANIZE."

### Reflection Question
Why are B-Trees "Shallow and wide" instead of "Deep and narrow"? (Hint: Think about the cost of a disk read).
