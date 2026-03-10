# Exercise 005 - Spot Instances & Fault-Tolerant Architecture

### Objective
The 90% discount. Master **Spot Instances** (AWS) or **Preemptible VMs** (GCP). Learn how to use "Spare Capacity" from cloud providers for a massive discount, while building applications that can handle a 2-minute "Termination Notice" without losing data or crashing.

### Core Concepts to Master
- **Spot Instance:** Unused cloud capacity available at up to 90% discount.
- **Interruption/Preemption:** When the cloud provider "Takes back" the server because a full-price customer needs it.
- **The Spot Market:** How the price of spot instances fluctuates based on global supply and demand.
- **Diversification:** Using multiple "Instance types" and "Regions" to increase the chance of keeping your spot capacity.

### Research Topics
- "Building a fault-tolerant workload using Spot instances"
- "AWS Spot Instance termination notice (How to catch it)"
- "Using Spot for CI/CD, batch processing, and stateless microservices"

---

### The Practical Challenge

**Part 1: The "Termination" Handler**
1. Research how and where AWS/GCP sends the "Termination Notice":
   - (AWS: Instance Metadata Service at `http://169.254.169.254/latest/meta-data/spot/instance-action`).
2. Write a script that "polls" this endpoint every 5 seconds. 
3. If a termination notice is detected, the script should:
   - Mark the server as "Draining" in the load balancer.
   - Upload any local logs or state to S3.
   - Send a Slack message: "I'm dying in 2 minutes, goodbye!".

**Part 2: Identifying "Spot-Friendly" Workloads**
1. Discuss which of these are safe for Spot:
   - A Customer Payment Database (SQL).
   - A Video Encoding Queue (FFmpeg).
   - A Jenkins CI Runner.
   - A High-Availability API Gateway.
2. (Answer: Video and Jenkins are perfect; DB and Gateway are risky).

**Part 3: Spot Fleet & Diversification**
1. Research **Spot Fleets**. 
2. Instead of asking for "10 x m5.large," you ask for "10 servers from [m5.large, m4.large, r5.large]."
3. Discuss why "Diversification" makes your fleet more stable during a supply shortage.

**Part 4: The Economics of Spot**
1. Calculate the cost of running a cluster of 100 servers on Spot vs. On-Demand for 24 hours.
2. Discuss: If your Spot cluster crashes once a day for 15 minutes, is the $5,000 savings per month worth the downtime? (Answer: Depends on the business!).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Assuming "Spot is always available." During a global event or a region-wide spike, the spot price can actually go *above* the On-Demand price, or the capacity can disappear entirely for hours.
- **Gotcha 2:** State on Disk. Spot instances are deleted when interrupted. Any data sitting on that server's local storage is GONE. Always save state externally (S3, DB, Redis).

### Reflection Question
How does using Spot Instances force an engineering team to write better, more "Stateless" and "Resilient" code?
