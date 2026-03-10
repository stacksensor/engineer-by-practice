# Exercise 001 - Batch vs. Stream Processing

### Objective
Real-time vs. The Past. Master the fundamental difference between **Batch Processing** (Processing large chunks of data at once, usually overnight) and **Stream Processing** (Processing data as it arrives, usually within milliseconds). Learn when to wait for the "Day's End" and when to act "Right Now."

### Core Concepts to Master
- **Batch Processing:** High throughput, high latency. E.g., "Calculate the total sales for yesterday." (Tools: Spark, SQL, MapReduce).
- **Stream Processing:** Infinite, continuous data. Low latency, lower throughput. E.g., "Detect a fraudulent credit card transaction happening now." (Tools: Flink, Kafka Streams, Spark Streaming).
- **Bounded vs. Unbounded Data:** Batch works on "finished" data (Bounded); Stream works on data that "never ends" (Unbounded).
- **Micro-batching:** A hybrid approach (used by Spark Streaming) that processes tiny batches every 1 second.

### Research Topics
- "Batch vs Stream Processing: Use cases"
- "The concept of 'Data at Rest' vs 'Data in Motion'"
- "Why can't everything be a Stream?"
- "The Lamdba Architecture vs Kappa Architecture"

---

### The Practical Challenge

**Part 1: The Fraud Detection Test**
1. You are building a system to detect credit card theft.
2. **Batch approach:** You run a script at 3 AM to find suspicious purchases from the day before.
3. **Stream approach:** You analyze every purchase as it hits the server.
4. Discuss: If a thief is currently buying 50 iPhones, which system saves the customer more money?

**Part 2: The Efficiency Math**
1. Imagine 1,000,000 records.
2. In **Batch**, you load all 1M into RAM/Disk and process them in 10 minutes.
3. In **Stream**, you process 1 record every 0.001 seconds.
4. Discuss: Which approach uses "Less" peak RAM? (Answer: Stream). Which approach has more "Overhead"? (Answer: Stream).

**Part 3: The Kappa Architecture (Concept)**
1. Research the **Kappa Architecture**. 
2. Discuss why it suggests that you don't need a Batch system at all—you can just "Replay" your stream from the beginning to calculate historical totals.

**Part 4: Identifying the tool for the job**
1. Which approach would you use for:
   - "Monthly payroll calculation" (Answer: Batch).
   - "Uber driver location updates on a map" (Answer: Stream).
   - "Ranking the top 10 most popular songs of all time" (Answer: Batch).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Complexity. Stream processing is harder to debug and "Manage" than batch. If a stream crashes at 2 PM, you have to worry about the "Backlog" that builds up until 3 PM.
- **Gotcha 2:** Late Arrival. In Stream processing, what do you do if a "Purchase" event from 10 minutes ago arrives ONLY NOW? Batch systems don't have this problem because they wait until the end of the day.

### Reflection Question
Why is "Stream Processing" considered the only way to build a truly "Reactive" modern application? (Answer: Because users expect the UI to change the second an event occurs).
