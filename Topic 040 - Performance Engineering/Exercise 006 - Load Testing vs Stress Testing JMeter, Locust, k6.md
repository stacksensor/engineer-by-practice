# Exercise 006 - Load vs. Stress Testing (JMeter/k6)

### Objective
Break the system. Master **Load Testing** (Simulating expected traffic) vs **Stress Testing** (Simulating 10x traffic to see where it crashes). Learn how to use modern tools like **k6**, **JMeter**, and **Locust** to generate 10,000 requests per second and understand the difference between "Saturation" and "Collapse."

### Core Concepts to Master
- **Load Testing:** Can the app handle the 5,000 users we expect on Cyber Monday?
- **Stress Testing:** What happens if 50,000 users show up? Does the database stop working FIRST or does the web server?
- **Soak Testing:** Running 1,000 users for 24 hours to find a slow "Memory Leak."
- **Spike Testing:** Sending 10,000 users in 1 second.
- **Ramp-up:** Gradually increasing the users over 5 minutes.
- **Virtual Users (VUs):** Simulated clients that run in a loop.

### Research Topics
- "Load Testing vs Stress Testing: A clear comparison"
- "k6: The modern Cloud-Native load testing tool (using Javascript)"
- "Using JMeter for complex XML-based load tests"
- "Python-based load testing with Locust"

---

### The Practical Challenge

**Part 1: The "Expected" Load (Scenario)**
1. You work at a ticket site. You expect 10,000 users at 10:00 AM.
2. You run a **Load Test** with 10,000 VUs.
3. Observe:
   - Latency: 200ms.
   - CPU: 60%.
4. Result: **Success!**

**Part 2: The "Breaking" Stress (Scenario)**
1. You run a **Stress Test** with 50,000 VUs.
2. At 35,000 VUs, the database returns `Too many connections` errors.
3. At 40,000 VUs, the web server crashes.
4. Discuss: Where is your **"Saturation Limit"**? 
5. (Answer: 35,000 VUs). This tells you EXACTLY when to start "Panic-Scaling" on Cyber Monday.

**Part 3: Testing with k6 (Concept)**
1. Write a small script (JS): `export default function () { http.get('https://test.k6.io'); sleep(1); }`.
2. Research: How do you tell k6 to run with 100 users for 30 seconds? 
3. (Answer: `k6 run --vus 100 --duration 30s script.js`).
4. Look at the output. Find the **"P99"** metric.

**Part 4: Identifying the "Soak"**
1. Research **Memory Leaks**. 
2. Discuss why a "10-minute" load test won't find a memory leak, but a "24-hour" soak test will. 
3. (Answer: Because the leak only eats 1MB per hour, which doesn't matter for 10 minutes, but kills the server after 24 hours).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Testing in Production. Never run a load test against your live production site unless you want to get fired for accidentally DDoS-ing your own company! Always use a "Staging" environment that matches production hardware.
- **Gotcha 2:** The "Tester" Bottleneck. If the laptop running k6 is old, it might hit 100% CPU before the server does, giving you "Fake" results. Use a "Distributed" load test (multiple machines) for massive scale.

### Reflection Question
Why is "Spike Testing" (sending 1,000 users in 1 second) more difficult for a system to handle than a "Ramp-up" where 1,000 users arrive over 1 minute? (Answer: Because auto-scaling takes time to "Wake up" new servers, and caches need time to "Warm up").
