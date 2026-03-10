# Exercise 002 - Event Sourcing

### Objective
Stop storing "State" and start storing "History." Master the **Event Sourcing** pattern, where instead of overwriting a single row in a database, you store every single state change as an immutable record (an "Event"), allowing you to reconstruct the state of the system at any point in time.

### Core Concepts to Master
- **The Event Store:** An append-only database specifically designed to store ordered sequences of events.
- **Aggregates:** The business objects (e.g., an Order or a User) that are updated by events.
- **Projections:** Read-only views of the current state, built by replaying events from the store.
- **Snapshots:** A performance optimization that saves the current state of an aggregate every X events, preventing the need to replay thousands of events from the beginning of time.
- **Immutability:** Once an event is written, it can NEVER be changed or deleted.

### Research Topics
- "What is Event Sourcing and why use it?"
- "Event Sourcing vs CRUD"
- "Audit logging vs Event Sourcing"
- "Implementing Event Sourcing in Node.js or Python"

---

### The Practical Challenge

**Part 1: The Account Balance Example**
1. Traditional CRUD: Table `Accounts` has a column `Balance: 100`. If you withdraw $10, you change the number to `90`.
2. Event Sourced: You store 3 events:
   - `AccountCreated {initial: 0}`
   - `MoneyDeposited {amount: 100}`
   - `MoneyWithdrawn {amount: 10}`
3. Calculate the current balance by replaying the events.
4. Discuss: How do you find out *why* the balance is $90 in the CRUD model vs the Event Sourced model?

**Part 2: Handling Corrections**
1. Imagine the $10 withdrawal was a mistake. 
2. In CRUD, you just change the number back to 100.
3. In Event Sourcing, you cannot delete the mistake. You must add a NEW event: `WithdrawalCancelled {amount: 10}`.
4. Discuss the "Auditability" benefits of this approach.

**Part 3: Building a Projection (Code)**
1. Write a script that takes a list of JSON events representing a "Shopping Cart":
   - `{"type": "ItemAdded", "id": "apple", "price": 1}`
   - `{"type": "ItemAdded", "id": "banana", "price": 2}`
   - `{"type": "ItemRemoved", "id": "apple"}`
2. Process the list to output the final state: `{"cart": ["banana"], "total": 2}`.

**Part 4: Scaling with Snapshots**
1. If a user has been using your app for 5 years and has 1 million events, replaying them on every login is too slow.
2. Design a system that creates a "Snapshot" every 1000 events. 
3. Explain how you would reload the user's state using: `Last Snapshot + Events since that snapshot`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Versioning. If you change your schema (e.g., changing a field name from `price` to `cost`), your old events will be unreadable. You must handle "Event Upcasting" (translating old versions to new ones during the replay).
- **Gotcha 2:** Storage Growth. Storing every single change takes much more space than a simple CRUD table.

### Reflection Question
Why is Event Sourcing the standard architecture for complex Financial and Legal systems?
