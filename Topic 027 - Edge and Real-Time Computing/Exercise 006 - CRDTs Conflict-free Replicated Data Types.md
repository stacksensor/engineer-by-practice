# Exercise 006 - CRDTs (Conflict-free Replicated Data Types)

### Objective
Sync without a central master. Learn about **CRDTs (Conflict-free Replicated Data Types)**—data structures that can be updated independently and concurrently across different regions without coordination, and still be "Merged" into a consistent state automatically. Master the logic behind tools like **Figma** and **Google Docs**.

### Core Concepts to Master
- **The Synchronization Problem:** If two users in different regions update the same document at the exact same millisecond, who wins?
- **CRDT Properties:**
  - **Commutative:** The order of operations doesn't matter (A + B = B + A).
  - **Associative:** The grouping doesn't matter ((A + B) + C = A + (B + C)).
  - **Idempotent:** Applying the same operation twice has no effect (A + A = A).
- **G-Counter (Grow-Only Counter):** A simple CRDT where you can only add numbers.
- **LWW (Last Write Wins):** A simple (but risky) strategy where the person with the latest timestamp wins the conflict.

### Research Topics
- "What are CRDTs and how do they work?"
- "Implementing a collaborative text editor with Yjs or Automerge"
- "Convergent vs Commutative Replicated Data Types"

---

### The Practical Challenge

**Part 1: The G-Counter (Code/Logic)**
1. Imagine a distributed counter across 3 nodes (A, B, C).
2. Each node keeps its *own* sub-counter: `{A: 0, B: 0, C: 0}`.
3. Node A increments its value to 5. Node B increments its value to 10.
4. When they "Merge," the total is `Sum(5, 10, 0) = 15`. 
5. Discuss: Why does this never cause a conflict even if A and B update at the same time?

**Part 2: The Last-Write-Wins (LWW) Register**
1. Implement a simple "Value" store that includes a `timestamp`.
2. When merging two values, always pick the one with the higher timestamp.
3. Discuss the "Clock Skew" danger: What happens if the clock on Node A is 10 seconds ahead of Node B?

**Part 3: Collaborative Text (Conceptual)**
1. Research how **Figma** uses CRDTs to allow multiple designers to move the same square at the same time.
2. Discuss: If User A moves a square 10px Left and User B moves it 10px Right simultaneously, where should the square end up?

**Part 4: Offline Support**
1. Explain how CRDTs allow a user to edit a document while "Offline" (on a plane) and then merge their changes perfectly back into the "Online" version 4 hours later without overwriting their colleague's work.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Metadata Overgrowth. To keep track of history/conflicts, CRDTs often store extra metadata. Eventually, the metadata can become larger than the actual data itself! You need "Garbage Collection" to prune old history.
- **Gotcha 2:** Implementing your own. Building a bug-free CRDT for something complex like a rich-text editor is incredibly difficult. Always use an established library like `Yjs` or `Automerge`.

### Reflection Question
Why are CRDTs the "Holy Grail" for edge-first applications that need to support offline users and high-speed collaboration?
