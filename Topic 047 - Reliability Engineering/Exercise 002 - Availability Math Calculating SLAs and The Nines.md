# Exercise 002 - Availability Math: Calculating SLAs and "The Nines"

### Objective
Master the numbers. Learn how to calculate **Availability (Uptime)** and understand the technical and financial difference between "Three Nines" (99.9%) and "Five Nines" (99.999%).

### Core Concepts to Master
- **SLA (Service Level Agreement):** The *legal* contract with your customers (e.g., "We will be up 99.9% of the month").
- **Error Budget:** The 0.1% of "Permitted Failure" you have before you get sued or lose money.
- **The "Nines" Chart:** 
   - 99% = 3 Days/Year Down (Low Quality).
   - 99.9% = 8 Hours/Year Down (Standard).
   - 99.999% = 5 Minutes/Year Down (Mission Critical).
- **MTTR (Mean Time To Recovery):** If you only have 5 minutes of downtime a YEAR, why "Manual fixing" of servers is impossible.

### Research Topics
- "Calculating Uptime: The math of availability"
- "System Design: Achieving 99.999% availability"
- "The cost of downtime: Why 'The Nines' matter to Amazon"
- "The relationship between Reliability and Scalability"

---

### The Practical Challenge

**Part 1: The "Financial" Disaster (Scenario)**
1. You have a store that sells $1,000,000 of goods PER HOUR.
2. Your SLA is **99%**.
3. **The math:** 
   - 1% Down = 87 hours of "Down" per year.
   - **Loss:** 87 Hours * $1M = $87,000,000 LOST.
4. **The fix:** 
   - Research the cost to move to **99.99%** (52 minutes per year).
   - Discuss: If the new hosting costs $10M a year, but saves $80M in losses, is it a "Profit" or an "Expense"?
   - Answer: It is a massive profit. Reliablility is an *investment*.

**Part 2: The "Probability" Rule**
1. You have 2 Servers. Each has 90% Uptime.
2. **Setup A (Series):** Server 1 -> Server 2. If EITHER fails, you are down. (Math: 0.9 * 0.9 = 81% Uptime).
3. **Setup B (Parallel):** Server 1 || Server 2. You only fail if BOTH fail. (Math: 1 - (0.1 * 0.1) = 99% Uptime).
4. Discuss: Why does adding "Identical Servers" to a system make it 10x more reliable?

**Part 3: The "Five Nines" Problem**
1. Research **Five Nines (99.999%)**. 
2. Discuss why at this level, a human being cannot even "Log in" to a server before the SLA is broken.
3. Answer: Because 5 minutes a *year* means you must use **Self-Healing Automation** (Kubernetes, AWS Auto-scaling) that fixes the bug in milliseconds.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Uptime" Lies. A server might be "Up" (responds to PING) but "Broken" (100% of orders fail). (Solution: Track **Success Rate**, not just Pings).
- **Gotcha 2:** The 3 AM Bug. If a server fails at 3 AM and your engineer sleeps until 8 AM (5 hours), you just broke a **99.9%** (8h) Annual SLA in ONE night. (Solution: **On-call rotation** and PagerDuty).

### Reflection Question
Why is 100% Uptime technically and mathematically impossible in computer science? (Answer: Because of the 'CAP Theorem' and the fact that atoms, networks, and hardware eventually fail).
