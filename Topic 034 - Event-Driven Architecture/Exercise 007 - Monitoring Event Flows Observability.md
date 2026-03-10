# Exercise 007 - Monitoring Event Flows (Observability)

### Objective
Don't get lost in the noise. Master **Event-Driven Observability**. Learn how to track a single business action (like "Placing an Order") as it travels through 5 different queues and 10 different microservices. Understand **Correlation IDs**, **Distributed Tracing**, and **Consumer Lag monitoring**.

### Core Concepts to Master
- **Correlation ID:** A unique string (UUID) generated at the start of a request and passed in the "Header" of every event.
- **Distributed Tracing:** Tools like **Jaeger** or **Honeycomb** that visualize the timeline of a distributed request.
- **Consumer Lag:** The number of messages currently waiting in the queue. If lag is increasing, your system is failing to keep up.
- **Dead Letter Alerts:** Being notified the second an event fails multiple times.

### Research Topics
- "Distributed Tracing in Event-Driven Systems"
- "Monitoring Kafka Consumer Lag with Burrow or Prometheus"
- "The concept of 'Span' and 'Trace' in OpenTelemetry"
- "Log Aggregation for asynchronous services"

---

### The Practical Challenge

**Part 1: The Correlation ID trace**
1. Search your logs (or imagine doing so) for all lines containing `trace_id=abc-123`.
2. You see:
   - `[Service A] Received HTTP Req. Emitting Event 1.`
   - `[Service B] Received Event 1. Calling DB.`
   - `[Service C] Received Event 1. Sending Email.`
3. Discuss: If Service C failed, how would you find the original HTTP request from Service A without this ID?

**Part 2: Calculating Lag**
1. Producer speed: 100 messages/second.
2. Consumer speed: 90 messages/second.
3. Calculate the "Lag" after 1 hour. (Answer: 10/sec * 3600 sec = 36,000 messages).
4. Discuss: How does this affect the "Real-time" feel of the app? (Answer: Users will wait 6 minutes for their "Order Confirmed" email).

**Part 3: The Dashboard Design**
1. Draw a dashboard for an Event-Driven system. Which 3 metrics are the most important?
   - (Answer: 1. Total Lag per queue, 2. Throughput (Events/sec), 3. Error rate/DLQ count).

**Part 4: OpenTelemetry (Conceptual)**
1. Research how **OpenTelemetry** can "Inject" headers into a Kafka message automatically.
2. Discuss why this is better than manually adding headers in every `if/else` block of your code.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Clock Skew. If Service A and Service B have different "Times," your trace will look like the event was received 5 minutes *before* it was sent. Use NTP to keep clocks in sync!
- **Gotcha 2:** Logging too much. In a high-traffic system (10k events/sec), logging EVERY single event can actually slow down the system and cost thousands of dollars in log storage fees. Use **Sampling** (e.g., trace only 1% of events).

### Reflection Question
Why is "Consumer Lag" often a better predictor of a system outage than "CPU Usage" in an Event-Driven Architecture? (Answer: Because CPU can look fine while the system is quietly failing to process the backlog of work).
