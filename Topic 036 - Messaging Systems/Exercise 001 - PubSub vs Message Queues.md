# Exercise 001 - Pub/Sub vs. Message Queues

### Objective
Define the delivery style. Master the two most common communication patterns in distributed systems: **Pub/Sub (Publish-Subscribe)** and **Message Queues (P2P)**. Learn the difference between "One-to-Many" (Broadcasting) and "One-to-One" (Task Distribution), and understand when to use each for your application.

### Core Concepts to Master
- **Message Queue (Point-to-Point):** A message travels from 1 producer to 1 consumer. Once read, it’s gone. Essential for "Work Distribution."
- **Pub/Sub (Publish-Subscribe):** A message travels from 1 producer to MANY subscribers. Each subscriber gets their own copy. Essential for "Broadcasting State Changes."
- **Topic:** The logical channel for Pub/Sub.
- **Queue:** The logical channel for task management.

### Research Topics
- "Pub/Sub vs Message Queues: A comparison"
- "Broadcast patterns in distributed systems"
- "When would I use BOTH in the same app?"
- "Fan-out: Distributing one message to multiple queues"

---

### The Practical Challenge

**Part 1: The "Work" Scenario (Queue)**
1. You have 3 workers and 9 "Image Resize" tasks.
2. If you use a **Queue**, how many tasks does each worker get? (Answer: ~3 tasks each).
3. Discuss: Is it efficient for all 3 workers to resize the SAME image? (Answer: No).

**Part 2: The "Notification" Scenario (Pub/Sub)**
1. You have 3 services: `Email`, `SMS`, and `Analytics`.
2. A user signs up.
3. If you use **Pub/Sub**, how many copies of the `UserSignedUp` event are sent? (Answer: 3 copies, one to each service).
4. Discuss: If tomorrow you add a `Slack` service, do you need to change the `Producer` code? (Answer: No, the new service just "Subscribes").

**Part 3: The Hybrid Model**
1. Research how **RabbitMQ** uses a **Fan-out Exchange** to turn one message into multiple queues.
2. Draw a diagram showing a single "Order Created" message ending up in 4 separate worker queues.

**Part 4: Identifying the pattern**
1. Which pattern for:
   - "Processing credit card payments" (Answer: Queue).
   - "Updating a real-time leaderboard for 1,000 players" (Answer: Pub/Sub).
   - "Sending a daily newsletter to 1 million people" (Answer: Pub/Sub).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Subscribers arriving late. In a "Pure" Pub/Sub system, if a subscriber wasn't listening when the message was sent, they miss it forever.
- **Gotcha 2:** Load Balancing. If you accidentally use Pub/Sub for "Work," you might have 5 servers all tried to charge the SAME customer at the same time!

### Reflection Question
Why is Pub/Sub considered the most "Scalable" way to grow a software team? (Answer: Because team B can start listening to team A's messages without ever talking to team A).
