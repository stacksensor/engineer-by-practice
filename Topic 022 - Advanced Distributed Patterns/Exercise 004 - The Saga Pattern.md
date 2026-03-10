# Exercise 004 - The Saga Pattern (Distributed Transactions)

### Objective
Maintain consistency across microservices. Learn how to manage long-running business processes that span multiple databases without using slow "Two-Phase Commit" protocols. Master the **Saga Pattern** to ensure that if one step in a multi-service chain fails, the previous steps are automatically "Undone" using compensating transactions.

### Core Concepts to Master
- **The Microservice Transaction Problem:** Each microservice has its own private database. How do you "Roll back" an order if the shipping service fails but the payment service has already taken the money?
- **Choreography-based Saga:** Services communicate via events (e.g., Service A finishes and publishes an event that Service B listens to).
- **Orchestration-based Saga:** A central "Saga Manager" manages the logic and tells each service what to do.
- **Compensating Transactions:** The "Undo" action for every successful step (e.g., a "Refund" is the compensating transaction for a "Payment").

### Research Topics
- "The Saga Pattern for microservices"
- "Choreography vs Orchestration Sagas"
- "Dealing with distributed transactions without 2PC"

---

### The Practical Challenge

**Part 1: The Booking Workflow**
1. Imagine an app to "Book a Trip":
   - Step 1: Book Flight (Service A)
   - Step 2: Book Hotel (Service B)
   - Step 3: Book Car (Service C)
2. Workflow: User starts the booking -> A succeeds -> B succeeds -> C FAILS (no cars available).
3. Discuss: In a Monolith, you use `ROLLBACK`. In Microservices, the Flight and Hotel are already booked!

**Part 2: Designing the Compensations**
1. Define the "Undo" action for each step:
   - Flight: `CancelFlight` (and refund credit).
   - Hotel: `CancelRoom` (and release inventory).
2. Trace the **Choreography** flow:
   - Service C fails and publishes `CarBookingFailed`.
   - Service B hears this and runs `CancelRoom`. When finished, it publishes `HotelBookingCancelled`.
   - Service A hears this and runs `CancelFlight`.

**Part 3: The Orchestrator (Code/Logic)**
1. Design a central "Workflow Manager" (using a state machine) that keeps track of the trip status.
2. The manager sends a command to Service A. It waits for the result. 
3. If successful, it sends a command to Service B.
4. Discuss why an **Orchestrator** is easier to debug than **Choreography** when your workflow has 20 complex steps.

**Part 4: Handling the "In-Between" State**
1. While the Saga is running, the Flight is booked but the Car is not.
2. If the user checks their "My Trips" page right then, what should they see? (e.g., "Pending", "Processing").
3. Discuss the "Semantic Lock" problem in distributed systems.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Non-Compensatable Actions. Some actions cannot be undone (e.g., sending an email or shipping a physical package). These must always be the *last* step of your Saga.
- **Gotcha 2:** The "Infinite Loop" Fail. If Service C fails and tries to undo Service B, but the undo action *also* fails, you are in a "Dangling State." You need a manual intervention process or a "Dead Letter Queue" for these cases.

### Reflection Question
Why are Sagas considered "Eventually Consistent" rather than "Atomic"?
