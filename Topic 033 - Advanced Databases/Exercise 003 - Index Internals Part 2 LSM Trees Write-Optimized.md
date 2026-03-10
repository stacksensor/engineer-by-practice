# Exercise 003 - Index Internals Part 2: LSM Trees (Write-Optimized)

### Objective
Master the "Big Data" index. Understand the **LSM (Log-Structured Merge-Tree)**—the data structure used by **Cassandra**, **ScyllaDB**, **RocksDB**, and **BigTable**. Learn why it is much faster for writing than a B-Tree and how it uses a combination of Memory (MemTable) and sorted disk files (SSTables) to achieve massive scale.

### Core Concepts to Master
- **MemTable:** An in-memory buffer (usually a skip-list or tree) where new data is written first.
- **SSTable (Sorted String Table):** An immutable, sorted file on disk.
- **Compaction:** The "Merge" process where multiple SSTables are combined, and old/deleted data is finally removed to save space and speed up reads.
- **Write Amplification:** The trade-off of writing the same data multiple times during compaction.
- **Bloom Filters:** A probabilistic data structure used to check "Is this data maybe in this file?" without reading the file.

### Research Topics
- "How LSM Trees work"
- "LSM Tree vs B-Tree: The performance trade-off"
- "What is an SSTable?"
- "The importance of Compaction in NoSQL databases"

---

### The Practical Challenge

**Part 1: The "Write-Only" Speed**
1. Research why writing to an LSM Tree is essentially an **Append** operation.
2. Discuss: Why is appending to a file/memory faster than "Updating" a B-Tree node in the middle of a disk?

**Part 2: The Reading Problem**
1. Imagine searching for a user in an LSM Tree. 
2. You first check the **MemTable** (Memory). Then you have to check **every single SSTable** on disk in reverse-chronological order.
3. Discuss: If you have 50 SSTables, your read could be 50x slower than a B-Tree. How does a **Bloom Filter** fix this?

**Part 3: The Compaction Simulation**
1. File 1: `{id: 1, val: "A"}, {id: 2, val: "B"}`.
2. File 2: `{id: 1, val: "C"}` (This is an update to ID 1).
3. Merge them into File 3. What is the result? (Answer: `{id: 1, val: "C"}, {id: 2, val: "B"}`).
4. Discuss how "Deletions" are handled in LSM Trees (Hint: **Tombstones**).

**Part 4: Real-world identification**
1. List 3 databases that use B-Trees.
2. List 3 databases that use LSM Trees.
3. Discuss: Why would you pick an LSM-based database for a "Sensor Data" application?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Compaction Lag. If your "Write" speed is faster than your "Compaction" speed, your disk will fill up with old data, and your "Read" performance will collapse.
- **Gotcha 2:** The "Free Space" requirement. To compact a 10GB SSTable, you usually need at least another 10GB of free space on the disk to write the new merged file.

### Reflection Question
Why are LSM Trees the "Natural choice" for SSD-based storage systems compared to HDDs? (Hint: Sequential writes vs Random writes).
