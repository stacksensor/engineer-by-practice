# Exercise 003 - The "Chaos" Simulation: Failure Modes and Effects Analysis (FEMA)

### Objective
Break the machine. Learn to think like a "Chaos Engineer" by predicting how a single broken wire or a full database can crash your entire company. Use **FMEA** (Failure Mode and Effects Analysis) to audit your system before it fails.

### Core Concepts to Master
- **Single Point of Failure (SPOF):** The "Boss" server. If it dies, the whole company dies. 
- **The "Cascading" Failure:** When App A fails, starts retrying 1,000 requests to App B, and "Crushes" App B to death.
- **Circuit Breakers:** The "Fuse" that stops App A from killing App B.
- **Fail-Open vs. Fail-Closed:** 
   - **Fail-Open:** (Security) If the "Login" server is down, everyone is allowed in. (Bad).
   - **Fail-Closed:** If the "Login" server is down, NO ONE is allowed in. (Safer).

### Research Topics
- "Netflix Chaos Monkey: Why they kill their own servers"
- "Introduction to FMEA: Identifying risks in systems"
- "Cascading Failures in Distributed Systems: Prevention and recovery"
- "Post-Mortem Best Practices: Learning from the outage"

---

### The Practical Challenge

**Part 1: The "Boss" SPOF (Scenario)**
1. You have 1,000 App servers. But only **1 Database**.
2. **The "Chaos" Test:** You "Unplug" the database.
3. Discuss: How many of the 1,000 apps are now broken? (Answer: All 1,000).
4. **The fix:** 
   - Research **Multi-Region Failover**. 
   - Discuss: If the "Master" DB dies, how long until the "Backup" DB takes over? (Standard: 30 seconds).

**Part 2: The "Retries" Storm**
1. App A can't talk to App B.
2. App A is coded to "Retry every 1 millisecond."
3. **The Disaster:** After 1 minute, App A is sending **1,000,000** requests to a broken App B. 
4. **The fix:** 
   - Research **Exponential Backoff with Jitter**. 
   - Discuss: Why is "Waiting 1s, then 2s, then 4s" better than "Immediate Retry"?
   - Answer: Because it lets the broken server "Breathe" and fix itself.

**Part 3: The "Circuit Breaker" (Concept)**
1. Think of a real fuse in your house. 
2. Research the **Circuit Breaker** code pattern. 
3. Discuss: If App B is 100% down, why should App A "Stop even trying" for 1 minute?
4. Answer: To save CPU and Network costs, and to stop a "Cascading" total crash.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Zombie" Failures. A server that is "Slow" (takes 30 seconds to answer) is 10x WORSE than a server that is "Dead" (takes 0.1s to fail). (Solution: Always set **Timeouts**!).
- **Gotcha 2:** The "Invisible" SPOF. You have 2 servers, but they are both on the same "Power Strip" in the datacenter. (Solution: Check **Physical Redundancy**).

### Reflection Question
Why is "Testing for Success" only 10% of the job for a Senior Reliability Engineer? (Answer: Because 'Success' is easy; 'Failure' is where the complexity and the money occur).
