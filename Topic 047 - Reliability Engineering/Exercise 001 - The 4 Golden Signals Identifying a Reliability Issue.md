# Exercise 001 - The 4 Golden Signals: Identifying a Reliability Issue

### Objective
Watch the pulse. Master the **4 Golden Signals** (Latency, Traffic, Errors, and Saturation) defined by the Google SRE (Site Reliability Engineering) team. Learn how to monitor these metrics to distinguish between a "Fast healthy app," a "Slow healthy app," and a "Slow dying app."

### Core Concepts to Master
- **Latency:** The time it takes to service a request (ms).
- **Traffic:** The demand placed on your system (e.g., Requests/Sec).
- **Errors:** The rate of requests that fail (e.g., 5% fail with 500 errors).
- **Saturation:** How "Full" your system is (e.g., "The CPU is at 95% usage").
- **SLO (Service Level Objective):** "We will have 99.9% success rate."
- **SLA (Service Level Agreement):** The contract with the customer ("If we fail our SLO, we will pay you money").

### Research Topics
- "The 4 Golden Signals: Definitions and examples"
- "Monitoring System Saturation (CPU, RAM, Connections)"
- "SLI vs SLO vs SLA: A simple comparison"
- "The importance of 99th percentile (P99) for reliability"

---

### The Practical Challenge

**Part 1: The Outage Analysis**
1. System: 1,000 users/sec. 
2. Sudden change: CPU hits 100% (**Saturation**).
3. Result: Latency jumps from 50ms to 5,000ms (**Latency**).
4. Result: Users start getting "Timeouts" (**Errors**).
5. Discuss: Which signal "Caused" the outage? (Answer: Saturation). Which signal did the "User" notice first? (Answer: Latency).

**Part 2: The SLO Calculation**
1. You have 1,000,000 requests per month.
2. Your SLO is **99.9% Uptime**.
3. How many failed requests (or "Downtime minutes") are you allowed before you break your promise? 
4. (Answer: 1,000 failed requests or ~43 minutes of downtime).
5. Discuss: If you use up all 43 minutes in the first week, how do you change your work for the rest of the month? (Hint: **Error Budget**).

**Part 3: Identifying the Signal**
1. Which signal for:
   - "How many people are using the app right now?" (Answer: Traffic).
   - "How much free disk space is left on the DB server?" (Answer: Saturation).
   - "The average time it takes to resize an image." (Answer: Latency).

**Part 4: Identifying the "Critical" signal**
1. Discuss: If **Traffic** stays the same but **Latency** increases, is the app about to crash? (Answer: Likely, as saturation is probably hitting a limit).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Averaging the Averages. Never "Average" a latency metric over multiple servers; it will hide the broken one! Always look at the raw data (P99).
- **Gotcha 2:** Ignoring "Quiet" errors. If an API returns `200 OK` but the body says `{"error": "database failed"}`, your monitoring system might think everything is fine. You must monitor the **Actual Content** of results.

### Reflection Question
Why is "Saturation" the most important signal for predicting an outage before it happens? (Answer: Because it tells you how much "Room" you have left before the system starts slowing down).
