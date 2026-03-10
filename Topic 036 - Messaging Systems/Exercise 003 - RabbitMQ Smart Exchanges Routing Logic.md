# Exercise 003 - RabbitMQ: Smart Exchanges & Routing

### Objective
Master the "Post Office" of messaging. Understand **RabbitMQ**—a smart broker that uses **Exchanges**, **Bindings**, and **Routing Keys** to decide exactly where a message should go. Learn the difference between **Direct**, **Topic**, and **Fan-out** exchanges and why RabbitMQ is better for complex workflows than Kafka.

### Core Concepts to Master
- **The Exchange:** The entry point for a message. Producers send to exchanges, NOT queues.
- **The Queue:** The destination where messages sit and wait.
- **Binding:** The "Link" between an exchange and a queue.
- **Direct Exchange:** Delivers to a queue based on an exact match of a Routing Key (e.g., `error`).
- **Topic Exchange:** Delivers based on wildcard matches (e.g., `user.*.created`).
- **Fan-out Exchange:** Delivers to every single queue bound to it (Broadcast).

### Research Topics
- "RabbitMQ vs Kafka: Smart Broker vs Dumb Broker"
- "Wildcard routing in RabbitMQ topics"
- "AMQP (Advanced Message Queuing Protocol) overview"
- "The concept of 'Acknowledgements' (ACK) in RabbitMQ"

---

### The Practical Challenge

**Part 1: The Direct Match**
1. Exchange Name: `logs`. 
2. Queue A is bound with key `error`. Queue B is bound with key `info`.
3. You send a message with Routing Key `error`. Which queue gets it? (Answer: A).
4. You send a message with Routing Key `debug`. Which queue gets it? (Answer: Neither. The message is dropped or sent to a DLX).

**Part 2: The Wildcard Topic**
1. Exchange Name: `users`.
2. Queue A bound with `user.#` (everything starting with user).
3. Queue B bound with `user.created` (only created).
4. You send `user.created`. Which queues get it? (Answer: Both).
5. You send `user.deleted.v2`. Which queues get it? (Answer: Only A).
6. Discuss: How does this help you build a system where one team listens to "All User events" and another listens to "Only sign-ups"?

**Part 3: The "Durable" Promise**
1. Research the difference between a **Durable** queue and a **Transient** one. 
2. What happens if the RabbitMQ server restarts? (Answer: Transient queues and their messages are gone; Durable ones survive).

**Part 4: Identifying the use case**
1. Why is RabbitMQ better for "Background Jobs" than Kafka? 
2. (Answer: Built-in support for priorities, individual message acknowledgements, and flexible routing).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Unbounded" Queue. If you have no workers, and your producers keep sending messages, RabbitMQ will store everything in RAM until it crashes. You should always set a **Max Length** or **TTL**.
- **Gotcha 2:** Prefetch Count. If you set prefetch to `100` and one message takes 10 seconds to process, that one server is effectively "hogging" 99 other messages while they sit idle. Set prefetch to `1` for heavy tasks.

### Reflection Question
Why is the "Exchange" abstraction in RabbitMQ considered more flexible than the "Topic" abstraction in Kafka? (Answer: Because it allows for complex routing logic inside the broker rather than in the client).
