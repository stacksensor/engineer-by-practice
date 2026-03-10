# Exercise 001 - Request-Response vs. Event-Driven

### Objective
Shift your mindset. Master the fundamental difference between **Request-Response** (Synchronous, direct, coupled) and **Event-Driven Architecture (EDA)** (Asynchronous, indirect, decoupled). Learn when to "Ask" for something to happen and when to just "Announce" that something *did* happen.

### Core Concepts to Master
- **Synchronous (Request-Response):** Client waits for the server to finish. If the server is down, the client fails. (The "Restaurant Waiter" model).
- **Asynchronous (Event-Driven):** Service A emits an event and forgets about it. Service B reacts whenever it's ready. (The "Bulletin Board" model).
- **Temporal Decoupling:** The ability for the producer and consumer to be "Active" at different times.
- **Producer / Consumer / Broker:** The 3 primary actors in an EDA.

### Research Topics
- "Request-Response vs Event-Driven Architecture"
- "The concept of 'Fire and Forget'"
- "Pros and Cons of tight coupling vs loose coupling"
- "When to use a REST API vs a Message Queue"

---

### The Practical Challenge

**Part 1: The Coupling Audit**
1. Imagine an E-commerce app. A user clicks "Buy."
2. **Synchronous Flow:** Order Service calls Inventory Service, calls Shipping Service, calls Email Service.
3. **Event Flow:** Order Service emits `OrderPlaced` event. Inventory, Shipping, and Email services all listen for that event.
4. Discuss: If the "Email Service" is down for 10 minutes, what happens to the "Buy" button in both scenarios?

**Part 2: The Latency Win**
1. Calculate the total time for a user if:
   - Order process (50ms) + Email (500ms) + Shipping (200ms) = ??
2. Compare to the EDA version where the user only waits for the Order process (50ms) to finish.

**Part 3: The "Source of Truth" Dilemma**
1. In a synchronous world, the Order Service "knows" if the Email was sent. 
2. In an EDA world, how does the Order Service know if the Email failed? 
3. Discuss: Does the Order Service *need* to know? (Hint: The power of decoupling).

**Part 4: Real-world check**
1. List 3 scenarios where Request-Response is BETTER. (Example: ATM Withdrawal - you need to know the money is there *now*).
2. List 3 scenarios where Event-Driven is BETTER. (Example: Signing up for a newsletter).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Distributed Tracing. It's much harder to follow a single "User request" across 10 services if they are talking via an anonymous message queue.
- **Gotcha 2:** The "Event Storm." If you aren't careful, one event can trigger five others, which trigger ten others, until your system is doing thousands of units of work for a single mouse click.

### Reflection Question
Why does Event-Driven Architecture make "Scaling" a team of 100 developers much easier than a Request-Response architecture? (Answer: Teams don't have to wait for each other's APIs to be ready).
