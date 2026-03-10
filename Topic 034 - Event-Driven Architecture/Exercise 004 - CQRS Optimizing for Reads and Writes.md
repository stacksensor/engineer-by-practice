# Exercise 004 - CQRS: Optimizing for Reads and Writes

### Objective
Divide and conquer. Master **CQRS (Command Query Responsibility Segregation)**—the pattern of using different data models for "Writing" (Commands) and "Reading" (Queries). Learn how this allows you to scale your "Reads" infinitely without slowing down your "Writes" and vice-versa.

### Core Concepts to Master
- **The Command (Write):** An action that changes state (e.g., `PlaceOrder`). Usually handled by a relational database optimized for consistency.
- **The Query (Read):** A request for data (e.g., `GetOrderHistory`). Usually handled by a "Denormalized" database optimized for speed (like Elasticsearch or Redis).
- **The Synchronization Pipe:** The event bus that moves data from the "Write" side to the "Read" side.
- **Eventual Consistency:** Accepting that the "Read" side might be a few milliseconds (or seconds) behind the "Write" side.

### Research Topics
- "CQRS definition and use cases"
- "When NOT to use CQRS"
- "The relationship between CQRS and Event Sourcing"
- "Denormalization vs Normalization"

---

### The Practical Challenge

**Part 1: The Bottleneck Audit**
1. Imagine an app where 1,000 updates happen per second, but 1,000,000 reads happen per second.
2. If you use one SQL database, the complex JOINs for the "Reads" are slowing down the "Writes."
3. Discuss: How does CQRS solve this by moving the JOIN results into a separate "Read-only" table?

**Part 2: Designing a Read Model**
1. **Write Model (Normalized):** `Users` table, `Orders` table, `Products` table.
2. **Read Model (Denormalized):** A single JSON document in MongoDB/Elasticsearch containing everything for one order: `{id: 1, user_name: "Alex", product_title: "Phone", total: 100}`.
3. Discuss: Which model is faster for showing a user their "Order History" page?

**Part 3: The Eventual Consistency User Experience**
1. User clicks "Update Profile."
2. The **Write side** updates successfully.
3. The **Read side** hasn't updated yet.
4. The user refreshes the page and sees their OLD name.
5. Discuss: How do you handle this in the UI? (Hint: Optimistic UI updates or a small "Loading" delay).

**Part 4: Scaling the sides independently**
1. If your "Search" feature becomes extremely popular, do you need to buy a bigger "Write" database? 
2. (Answer: No, you just add more workers to the "Read" side).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Complexity. You now have two databases, two schemas, and a synchronization service. This is too much for a small startup.
- **Gotcha 2:** Synchronization Failure. If the event bus crashes, your Read side will stay "stale" forever until you manually fix it.

### Reflection Question
Why is CQRS almost always used in combination with Event Sourcing for high-performance systems? (Answer: Event Sourcing provides the perfect stream of data to build the Read models).
