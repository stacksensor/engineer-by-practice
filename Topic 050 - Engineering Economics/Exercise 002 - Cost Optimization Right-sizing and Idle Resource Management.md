# Exercise 002 - Cost Optimization: Right-sizing and Idle Resource Management

### Objective
Trim the fat. Learn to reduce your "Cloud Bill" by **Right-sizing** servers (using `t4g.small` instead of `m5.large`) and identifying "Ghost" resources that you are paying for but not using.

### Core Concepts to Master
- **Right-sizing:** Picking the 1 CPU server when your app only uses 10% CPU.
- **Idle Resources:** A "NAT Gateway" or "Elastic IP" that costs $30/month even if 0 bytes are sent.
- **Spot Instances:** Buying "Spare" AWS capacity for 70-90% discount. (Bad for Databases, Good for Batch Jobs).
- **The "Graveyard" Audit:** 
   - 1. **Unused EBS Volumes** (Storage without a compute server).
   - 2. **Old Snapshots** (Backups from 3 years ago).
   - 3. **Idle Load Balancers.**

### Research Topics
- "AWS Compute Optimizer: What it is and why to use it"
- "Spot Instances vs. Reserved Instances (RI): The math"
- "Cloud Custodian: Automating the deletion of idle resources"
- "The FinOps cycle: Inform, Optimize, and Operate"

---

### The Practical Challenge

**Part 1: The "10% CPU" Disaster (Scenario)**
1. You have 100 App servers. 
2. **The "Stat":** Every one of them has 90% "Free" CPU.
3. **The math:** 
   - Each costs $100/month. Total = $10,000.
4. **The fix:** 
   - Research **Right-sizing**. 
   - Discuss: If you move to a server that costs $20/month, how much is the "Annual Profit"?
   - Answer: $10,000 - $2,000 = $8,000 saved per month. **$96,000 saved PER YEAR.**

**Part 2: The "Spot" Gamble**
1. You run a "Video Encoder" that takes 1 hour.
2. In the AWS "Sale" (Spot), it costs $1.
3. In the AWS "Store" (On-demand), it costs $10.
4. **The Risk:** AWS can "Take back" the server in 2 minutes.
5. Discuss: Why is a "Video Batch" good for Spot? (Answer: Because you just 'Restart' the job if it dies).
6. Discussion: Why is a "Customer Login" bad for Spot? (Answer: Because the user will crash).

**Part 3: The "NAT" Bill**
1. Research the cost of an **AWS NAT Gateway**. 
2. Discuss why it is one of the most "Expensive" tiny boxes in the cloud.
3. Answer: Because it charges per HOUR and per GIGABYTE. 

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Cheap" is Slow. Moving from an `m5` (Intel) to a `t4g` (ARM) server might make your Java app 50% slower. (Solution: Always **Performance Test** before changing types!).
- **Gotcha 2:** The "Forgotten" Snapshot. You delete a server, but forget the 10 Snapshots of its disk. They will charge you forever. (Solution: Use **Life Cycle Policies**).

### Reflection Question
Why are "Engineering Economics" technically a part of "Clean Code"? (Answer: Because code that runs on $10/month is 'Cleaner' than code that requires $1,000/month for the same result).
