# Exercise 007 - Choosing the Right Messaging System

### Objective
Pick your weapon. Master the art of choosing the right messaging system based on your business requirements. Compare **Apache Kafka**, **RabbitMQ**, **Apache Pulsar**, and **NATS**. Understand the three main criteria: **Throughput**, **Latency**, and **Complexity**.

### Core Concepts to Master
- **Kafka:** High throughput, durable, infinite replay. Best for: Analytics, Stream Processing, Centralized Log.
- **RabbitMQ:** High complexity routing, priorities, smart broker. Best for: Complex workflows, Background tasks.
- **NATS:** Low latency, extremely lightweight. Best for: Microservice communication, IoT, Edge.
- **Pulsar:** Tiered storage (moving old data to S3), multi-tenancy. Best for: Large enterprises with many teams.

### Research Topics
- "Kafka vs RabbitMQ vs NATS: A feature matrix"
- "The cost of operating Kafka (Self-hosted vs Managed)"
- "Apache Pulsar's unique architecture (Compute vs Storage)"
- "Benchmarking messaging systems"

---

### The Practical Challenge

**Part 1: The Comparison Table**
| Feature | Kafka | RabbitMQ | NATS |
| :--- | :--- | :--- | :--- |
| **Max Throughput** | Very High | Medium | High |
| **Latency** | Medium | Low | Very Low |
| **Persistence** | Permanent | Usually Deleted | Optional |
| **Routing Logic** | Simple (Topics) | Very Complex | Simple (Subjects) |

**Part 2: Scenario Analysis**
1. Scenario A: "A Global Bank needs to track every currency trade for the last 10 years for auditing." (Answer: Kafka).
2. Scenario B: "An e-commerce app needs to send a welcome email, a discount code, and a text message whenever a user signs up. Each has different retry logic." (Answer: RabbitMQ).
3. Scenario C: "A multiplayer game needs to send player 'Position' updates 60 times a second. If a message is lost, it doesn't matter since the next one is coming in 1/60th of a second." (Answer: NATS).

**Part 3: The "Tiered Storage" Advantage**
1. Research **Apache Pulsar**. 
2. How does it save money compared to Kafka by moving 1-year-old messages to S3 automatically?

**Part 4: Estimating Complexity**
1. Discuss the "Operational Burden." 
2. Why should a 2-person startup choose **AWS SQS** or **NATS** instead of setting up a 3-node **Kafka** cluster? (Answer: Maintenance overhead).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-engineering. Don't use Kafka just because Netflix does. If you only move 100 messages a day, a simple SQL table or a Python queue is enough.
- **Gotcha 2:** The "Black Box" broker. If you don't understand how your broker handles failure (e.g., what happens if the disk fills up?), you will be helpless during a production outage.

### Reflection Question
Why is the "Team's Experience" often more important than the "Technical Benchmarks" when choosing a messaging system? (Answer: Because a poorly managed Kafka cluster is more dangerous than a well-managed RabbitMQ cluster).
