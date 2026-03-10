# Exercise 003 - Right-sizing & Idle Resource Management

### Objective
Trim the fat. Master the art of **Right-sizing**—ensuring that every resource you pay for is sized exactly for its workload. Learn how to identify "Zombie" resources (orphaned disks, idle load balancers) and how to automate the cleanup of "Non-production" environments after business hours.

### Core Concepts to Master
- **Over-provisioning:** Paying for a Large server when a Small one would do.
- **Under-utilization:** Resources that sit at <10% CPU usage for 90% of the time.
- **Storage Cleanup:** Identifying "Orphaned" Snapshots or EBS volumes that are no longer attached to any server but are still charging you every month.
- **Environment Schedules:** Turning off Dev/Staging environments at 7 PM and back on at 8 AM.

### Research Topics
- "AWS Instance Scheduler: Automating start/stop"
- "Identifying idle resources in AWS/GCP"
- "What is an 'Orphaned' EBS volume?"

---

### The Practical Challenge

**Part 1: The Instance Audit**
1. You have 10 servers (t3.xlarge) used for user testing. 
2. Monitoring shows their CPU usage never exceeds 5%. 
3. Research the cost difference between `t3.xlarge` and `t3.small`. 
4. Calculate the monthly savings if you "Right-size" all 10 servers.

**Part 2: The "After-Hours" Plan**
1. Design a script (using Python/Boto3 or JS/Cloud SDK) that:
   - Finds all EC2 instances with the tag `Env: Dev`.
   - Stops them at 19:00 UTC.
   - Starts them at 07:00 UTC.
2. Calculate the savings of running a server for 12 hours a day instead of 24 (Hint: 50% savings).

**Part 3: Cleaning the Attic (Storage)**
1. Research "Snapshots" in AWS/GCP. 
2. Discuss why keeping 3 years of daily backups for a "Test Database" is a waste of money.
3. Propose a "Retention Policy" (e.g., "Keep 7 days of daily snapshots, then delete").

**Part 4: Identifying "Zombies"**
1. Research how an "Elastic IP" or a "Static IP" can cost you money even if it's NOT being used.
2. Discuss: Why does the cloud provider charge you for "Not using" a resource in this specific case? (Answer: Because IPs are a limited globally shared resource).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Sudden Peak." If you down-size a server too much, it might crash during a small spike in traffic. Always look at "Peak" metrics, not just "Average" metrics.
- **Gotcha 2:** State Loss. Before turning off an environment on a schedule, ensure it's "Stateless" or that the database can survive a hard stop.

### Reflection Question
Why is "Right-sizing" a continuous process rather than a one-time task?
