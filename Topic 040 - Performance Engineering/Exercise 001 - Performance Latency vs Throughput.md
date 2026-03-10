# Exercise 001 - Performance: Latency vs. Throughput

### Objective
Define the speed. Master the two most important metrics in **Performance Engineering**: **Latency** (The time for one request) and **Throughput** (The number of requests per second). Learn how to identify which one is the "Bottleneck" for your application and understand why improving one often makes the other worse.

### Core Concepts to Master
- **Latency (Response Time):** The "End-to-end" time for a single action (e.g., "50ms for a search result").
- **Throughput (Bandwidth):** The "Total Volume" of data or requests (e.g., "1,000 requests per second").
- **The "Highway" Analogy:**
  - **Latency:** How fast one car can drive (60 mph).
  - **Throughput:** How many cars can fit on the road at once (8 lanes).
- **The P99 (99th Percentile):** The time that 99% of your users experience. Why is the "Average" (P50) a lie?

### Research Topics
- "Latency vs Throughput: A comparison"
- "Understanding P50, P90, P95, and P99 metrics"
- "The concept of 'Tail Latency'"
- "Identifying a CPU-bound vs IO-bound bottleneck"

---

### The Practical Challenge

**Part 1: The "Average" Lie**
1. 10 Users request a page.
2. Latencies: `50ms, 52ms, 48ms, 51ms, 50ms, 49ms, 50ms, 51ms, 52ms, 5000ms`.
3. Calculate the **Average** (Mean): (Answer: ~545ms).
4. Calculate the **P90** (90th Percentile): (Answer: 52ms).
5. Discuss: Does the "Average" represent reality? Which number does the "Angry User" care about?
6. (Answer: The 1 user with 5,000ms is the most important one to fix, but the "Average" hides them!).

**Part 2: The Bottleneck Analysis**
1. Scenario: You add 10 more Lanes to your "Highway" (More servers). 
2. Discuss why this doesn't make a single request arrive any "Faster" (Latency stays same), but it allows شما to handle 10x more users (Throughput increases).

**Part 3: The Latency Penalty of "Features"**
1. Your app takes 100ms. You add "Security Scan" (+20ms), "Logging" (+10ms), and "Analytics" (+50ms).
2. Calculate the new Latency. (Answer: 180ms).
3. Discuss: Is your app "Slow," or is it "Feature-rich"?

**Part 4: Identifying the "Golden Signal"**
1. Research the **4 Golden Signals** (Google SRE Book):
   - Latency, Traffic, Errors, Saturation.
2. Choose one and explain how a spike in that signal would "Kill" your app.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Measuring on Localhost. Latency on your own machine is 0.001ms. Latency for a user in Japan talking to a server in NYC is 200ms. Always test "Over the network."
- **Gotcha 2:** The "Cold Start." The very first request to a Java or Lambdas function is always 10x slower than the second. Don't measure "Cold Starts" as your typical P50!

### Reflection Question
Why is "Throughput" easier to fix (by "throwing money/servers at it") compared to "Latency" (which requires rewriting code)? (Answer: Horizontal scaling vs Algorithmic efficiency).
