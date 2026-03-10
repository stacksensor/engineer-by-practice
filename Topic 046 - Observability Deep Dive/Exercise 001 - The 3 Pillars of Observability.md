# Exercise 001 - The 3 Pillars of Observability

### Objective
Expose the "Internal State" of your system. Master the three fundamental tools for **Observability**: **Logs** (What happened?), **Metrics** (How many/how long?), and **Traces** (Where did it start and end?). Learn how to combine them to solve complex production bugs in minutes instead of hours.

### Core Concepts to Master
- **Metrics:** Numerical data (Counter, Gauge, Histogram) for high-level monitoring. (e.g., "99th Percentile Latency is 100ms").
- **Logs:** Text-based records of specific events. (e.g., "User Alex clicked 'Buy' at 1:04 PM").
- **Traces:** A detailed timeline of a single request as it travels through multiple services. (e.g., "Order Service took 50ms, Payment Service took 1,000ms").
- **The "High Cardinality" problem:** Why you shouldn't put a "Single User ID" into your Metrics system. (Metrics are for groups; Logs are for individuals).

### Research Topics
- "Logs vs Metrics vs Traces: A comparison"
- "Monitoring vs Observability: What's the difference?"
- "The concept of 'Telemetry' data"
- "Tools for each pillar: (Prometheus, Kibana, Jaeger, Honeycomb)"

---

### The Practical Challenge

**Part 1: The Outage Scenario (Mystery)**
1. "Users are seeing errors."
2. **Metrics check:** You see a spike in `HTTP 500` errors on the **Orders Dashboard**.
3. **Trace check:** You look at one failed `Trace` and see the **Payment Service** returned an error.
4. **Log check:** You search for the `Trace ID` in the Payment Service logs and find: `Error: API Key Expired`.
5. Discuss: Could you find this with "Only Logs"? (Answer: Yes, but you'd have to search 1,000,000 lines manually). Could you find this with "Only Metrics"? (Answer: No, you'd only see the error, but not the *reason* why).

**Part 2: Designing a Metric**
1. You want to track "How many logins happen every minute."
2. Research: Is this a **Counter** or a **Gauge**? (Answer: Counter).
3. Discuss why you would want a **Histogram** (rather than just an Average) to see the speed of logins.

**Part 3: The Trace ID (Connection)**
1. Research how **Correlation IDs** are used to link a Log, a Metric, and a Trace together.
2. Discuss why a "Disconnected" log is 90% less useful than a "Trace-aware" log.

**Part 4: Identifying the pillar**
1. Which pillar for:
   - "A chart of CPU usage over 24 hours" (Answer: Metrics).
   - "A list of every user who entered an invalid password" (Answer: Logs).
   - "Seeing why one specific order took 10 seconds to finish" (Answer: Traces).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Firehose" of Logs. If you log 1,000 lines per second, your log storage (Elasticsearch/S3) will cost more than your actual application! Use "Sampling" for traces and "Summarization" for metrics.
- **Gotcha 2:** Only watching the "Summary" dashboard. An app can have 1% errors (which looks fine on a "99% Success" dashboard), but for those 1% of users, the app is 100% broken.

### Reflection Question
Why is Observability considered the "Only way" to manage a large microservice architecture? (Answer: Because it is impossible for a human to understand the "Map" and the "Health" of 50 different services without automated telemetry).
