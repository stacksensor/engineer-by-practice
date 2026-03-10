# Exercise 007 - SRE Game Day (Chaos Engineering)

### Objective
Build "Antifragile" systems. Instead of hoping things don't break, you will intentionally "break" your production-like environment (Chaos Engineering) to test your alerting, your dashboards, and your human response time. Learn how to build systems that can automatically survive a server crash.

### Core Concepts to Master
- **Chaos Engineering:** The discipline of experimenting on a software system in production to build confidence in its capability to withstand turbulent conditions.
- **MTTR (Mean Time To Recovery):** The average time it takes for your system (or your team) to fix a failure once it has been detected.
- **Failover:** The automatic switching to a redundant or standby computer server, system, hardware component or network upon the failure or abnormal termination of the previously active system.
- **Redundancy:** Having multiple copies of your data (Database Replication) and your code (Server Clusters) to avoid a single point of failure.

### Research Topics
- "Principles of Chaos Engineering"
- "Netflix Chaos Monkey explained"
- "How to perform a Game Day for SRE teams"
- "Designing for failure in the cloud"

---

### The Practical Challenge

**Part 1: The Setup**
1. Ensure you have Topic 16 Exercise 003 (Monitoring/Grafana) and Topic 16 Exercise 005 (Blue-Green/Load Balancer) running.
2. Your system should consist of:
   - 2 Web Servers.
   - 1 Load Balancer.
   - 1 Monitoring Dashboard with Alerts.

**Part 2: The Attack (The Game Day)**
1. Close your eyes (or have a friend do this).
2. Manually "Kill" one of your web server containers: `docker stop server-a`.
3. Start a timer.
4. Check your Monitoring Dashboard. How many seconds until the "Alert" triggers?
5. Visit your public URL. Does the site still work? (It should, if the Load Balancer is healthy-checking correctly).

**Part 3: The Recovery**
1. Attempt to "Fix" the issue. Start the server back up.
2. Observe the Load Balancer. Does it automatically start sending traffic back to the recovered server?
3. How long did the entire recovery take? This is your MTTR.
4. Discuss how you could automate the *restart* using a process manager like **PM2** or a container orchestrator like **Kubernetes**.

**Part 4: The Database Crash**
1. This is the hardest test. Intentionally stop your Database container.
2. Observe the app. It will likely crash completely.
3. Discuss "High Availability" (HA) databases. Instead of one DB, you have a "Primary" and a "Replica."
4. If you had a replica, could your app switch to "Read-Only Mode" while the primary database was being restored?
5. Write a "Post-Mortem" report. What was the root cause? How did the system respond? What can we build to make the next crash less painful?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Breaking something you can't fix. Always perform Chaos Experiments in a "Staging" or "Dev" environment first. Never run your first Game Day on a Friday afternoon!
- **Gotcha 2:** Ignoring the "Blast Radius." Start by breaking small, non-critical components before you attempt to kill your main database.

### Reflection Question
Why is "Designing for Failure" considered more realistic than "Designing for Perfection" in modern web scale engineering?
