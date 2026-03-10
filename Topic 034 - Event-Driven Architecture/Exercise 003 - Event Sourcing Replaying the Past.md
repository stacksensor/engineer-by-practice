# Exercise 003 - Event Sourcing: Replaying the Past

### Objective
Forget the current state; focus on the journey. Master **Event Sourcing**—a pattern where you store every *change* to the state as an immutable event, rather than just storing the final result in a database row. Learn how this provides a perfect audit log and the ability to "Time Travel" to any point in the system's history.

### Core Concepts to Master
- **The Event Store:** A database optimized for appending immutable events (e.g., EventStoreDB, or a Kafka topic).
- **Projections:** The process of reading the "Event Stream" and building a readable "Current State" (e.g., a SQL table representing a user's balance).
- **Snapshots:** Saving the "Current State" every 1,000 events so you don't have to replay 1 million events every time you start the app.
- **Immutability:** Once an event is saved (e.g., `MoneyWithdrawn`), it can NEVER be deleted or changed. To fix a mistake, you must issue a "Compensating Event" (`MoneyDeposited`).

### Research Topics
- "Event Sourcing vs CRUD"
- "Building a projection from an event stream"
- "When to use Snapshots in Event Sourcing"
- "The power of 'Time Travel' debugging"

---

### The Practical Challenge

**Part 1: CRUD vs Event Sourcing (The Bank)**
1. **CRUD Approach:** `UPDATE accounts SET balance = 100 WHERE id = 1;`.
2. **Event Sourcing Approach:**
   - `Event 1: AccountOpened (Initial: 0)`
   - `Event 2: MoneyDeposited (+150)`
   - `Event 3: MoneyWithdrawn (-50)`
3. Discuss: If the "Balance" in the CRUD approach is wrong, how do you know why? 
4. If you use Event Sourcing, can you ever "lose" the reason why the balance changed?

**Part 2: Designing a Projection**
1. Imagine an event stream of `UserJoined`, `UserUpdatedName`, `UserChangedEmail`.
2. Write a pseudocode "Projection" that loops through these events and creates a final `User` object.
3. Discuss: If tomorrow you decide you want to track "How many times users change their name," how does Event Sourcing help you calculate that for the last 5 years of data?

**Part 3: The Snapshots Necessity**
1. You have a "Counter" that has been incremented 10,000,000 times over 5 years.
2. Discuss why the app startup would be slow if you had to "Replay" all 10 million events every morning.
3. (Answer: Snapshots allow you to start from the state at 9,999,000 and only replay the last 1,000).

**Part 4: The Immutable Law**
1. Someone accidentally deposits $10,000 into an account.
2. In Event Sourcing, you are NOT allowed to delete that event. 
3. How do you fix it? (Answer: Add a new event: `Correction_MoneyWithdrawn (-10,000)`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Versioning Events. If you change the "Schema" of an event (e.g., changing `name` to `first_name`, `last_name`), your old code might not be able to "Replay" the old events.
- **Gotcha 2:** Consistency. It is very hard to ensure "Unique Email Address" in an Event Sourcing system because the "Event Store" doesn't know about the current state of other accounts.

### Reflection Question
Why is Event Sourcing the preferred choice for high-compliance industries like Banking, Healthcare, and Logistics? (Answer: Built-in audit trail).
