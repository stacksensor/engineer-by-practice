# Exercise 006 - Watermarking & Late-Arriving Data

### Objective
Respect the lag. Master **Watermarking**—the technique used to handle "Late" or "Out-of-Order" data in a streaming system. Learn how to tell the engine "Wait 10 seconds for any stragglers, then close the window and calculate the result." Understand the difference between **Event Time** and **Processing Time**.

### Core Concepts to Master
- **Event Time:** When the action actually happened (e.g., 2:00 PM on the user's phone).
- **Processing Time:** When the message arrived at your server (e.g., 2:05 PM due to bad Wi-Fi).
- **Watermark:** A timestamp sent in the stream that says "We believe there is no data older than X coming after this."
- **Skew:** The time difference between Event Time and Processing Time.
- **Allowed Lateness:** How long to keep a window "open" just in case very late data arrives.

### Research Topics
- "The concept of Watermarks in Apache Flink"
- "Event Time vs Processing Time vs Ingestion Time"
- "How to handle out-of-order events"
- "Setting an 'Allowed Lateness' policy"

---

### The Practical Challenge

**Part 1: The Out-of-Order Puzzle**
1. Events happen: `E1 (12:00)`, `E2 (12:01)`, `E3 (12:02)`.
2. Arrival order at server: `E1 (12:03)`, `E3 (12:04)`, `E2 (12:05)`.
3. If you use **Processing Time**, W1 contains E1, W2 contains E3, W3 contains E2. 
4. If you use **Event Time**, W1 contains all three.
5. Discuss: Why is "Event Time" the only way to get a mathematically "Correct" total for business data?

**Part 2: Defining the Watermark**
1. Policy: `Watermark = Max Event Time seen - 10 seconds`.
2. Current Max Event Time: `12:00:30`. Watermark is at `12:00:20`. 
3. An event arrives from `12:00:15`. Is it accepted? (Answer: Yes, it is "Behind" the watermark).
4. An event arrives from `12:00:05`. Is it accepted? (Answer: No, it is "Late". The engine has already closed that window!).

**Part 3: The "Wait" Trade-off**
1. Discuss: If you set your watermark delay to 1 hour (to be 100% safe), what happens to your "Real-time" dashboard? 
2. (Answer: All your charts will be 1 hour behind "Now").

**Part 4: Dealing with Dropped Data**
1. Research the "Side Output" pattern. 
2. Discuss why moved "Late/Dropped" data to a separate error topic (rather than just deleting it) is critical for high-stakes data like audit logs.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Idle Sources. If one partition of your Kafka topic stops sending data, the "Global Watermark" will get stuck, and none of your windows will ever close! (Note: Search for "Idleness detection" to fix this).
- **Gotcha 2:** Bad Device Clocks. If a user sets their phone to the year 2099, their "Event Time" will advance your watermark to 2099, instantly killing all other data! You must "Sanitize" and "Clamp" incoming timestamps.

### Reflection Question
Why are watermarks essentially a "Guess" or a "Probability" rather than an absolute guarantee? (Answer: Because in a distributed world, you can never be 100% sure a very slow packet isn't still coming).
