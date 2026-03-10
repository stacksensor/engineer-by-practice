# Exercise 006 - Competing Consumers & Load Balancing

### Objective
Divide the work. Master the **Competing Consumers** pattern. Learn how multiple instances of a service can "Compete" for messages in a queue to ensure high availability and high scale. Understand how the broker ensures that a message is only processed once, and how it handles a consumer that "Disappears" mid-task.

### Core Concepts to Master
- **The Queue as a Buffer:** Allowing the producer to "Speed up" without overwhelming the consumers.
- **Round Robin:** The broker giving one message to Consumer A, the next to Consumer B.
- **Acknowledge (ACK):** The signal from the consumer to the broker saying "I'm done, you can delete the message now."
- **Negative Acknowledge (NACK) / Requeue:** Telling the broker "I failed, give this message to someone else."
- **Visibility Timeout:** The time a broker hides a message while waiting for an ACK. If time runs out, the message becomes visible to others again.

### Research Topics
- "The Competing Consumers pattern"
- "Message acknowledgements in RabbitMQ vs SQS"
- "Horizontal scaling of message consumers"
- "Handling 'Zombie' consumers"

---

### The Practical Challenge

**Part 1: The Parallel Resize**
1. You have a queue with 100 images to resize.
2. 1 worker takes 100 seconds (1s per image).
3. 5 workers take 20 seconds.
4. Discuss: Why does this make "Scaling" as simple as spinning up more Docker containers?

**Part 2: The "Failure" Recovery**
1. Worker A takes a message to "Charge $100."
2. Worker A's power cord is pulled before it finishes.
3. Discuss: How does the Broker know to give that *same* message to Worker B after a 30-second wait? 
4. (Answer: The "Visibility Timeout").

**Part 3: The "Double Charge" Risk**
1. Discuss: What if Worker A finishes the charge, but the power dies *just before* it sends the ACK? 
2. Worker B gets the message and charges the customer again.
3. How do you solve this? (Hint: **Idempotency**).

**Part 4: Identifying the load balancing**
1. Research how **Kafka** load balances using "Consumer Groups" vs how **RabbitMQ** does it using "Single Queue Round Robin."
2. Which one allows you to have MORE consumers than partitions? (Answer: RabbitMQ).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Slow Worker" problem. If you have 4 fast workers and 1 extremely slow worker, 20% of your messages will be delayed simply because they were assigned to the "Wrong" worker.
- **Gotcha 2:** Prefetch limit. If one worker asks for 50 messages at once, it "blocks" other workers from helping out if it gets stuck on one difficult message.

### Reflection Question
Why is a Message Queue better for load balancing than a standard HTTP Load Balancer when the tasks take a long time (e.g., 5 minutes per task)? (Answer: Because the queue naturally "buffers" and waits for workers to be ready).
