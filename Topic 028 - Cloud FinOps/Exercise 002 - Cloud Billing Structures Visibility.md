# Exercise 002 - Cloud Billing Structures & Visibility

### Objective
Follow the money. Master the complex world of cloud bills (AWS Bill, GCP Billing). Learn how to use **Tags** and **Labels** to attribute costs to specific teams, projects, or environments (Dev vs Prod), and learn how to use "Cost Explorer" to identify exactly which service is driving your bill up.

### Core Concepts to Master
- **Billing Dimensions:** Region, Service, Data Transfer, Compute, and Storage.
- **Cost Allocation Tags:** Key-value pairs attached to resources to track who is spending what.
- **Invoice vs. Actual Cost:** Understanding the difference between what you are charged and the "Unblended" cost of your usage.
- **Cost Explorer / Billing Dashboards:** Tools used to visualize trends and anomalies.

### Research Topics
- "AWS Cost Allocation Tags best practices"
- "How to use GCP Billing Reports"
- "Identifying hidden costs in cloud (Data Transfer, NAT Gateways)"

---

### The Practical Challenge

**Part 1: The Tagging Policy**
1. Design a standard "Resource Tagging Policy" for a company with 3 teams (Alpha, Beta, Gamma).
2. It MUST include tags for: `Project`, `Team`, `Env` (Dev/Prod), and `CreatedBy`.
3. Discuss: If a resource has no tags, how do we know who to "Charge" for it at the end of the month?

**Part 2: The Mystery Spike**
1. You see a $500 spike in your bill yesterday.
2. In Cost Explorer, you filter by "Service." All services look normal except **"Data Transfer."**
3. Research the "Data Transfer" costs between AWS Regions vs Availability Zones.
4. Discuss: How could moving a database from `us-east-1` to `us-west-2` while the app stays in `us-east-1` cause this spike?

**Part 3: NAT Gateway - The Silent Killer**
1. Research the cost of an AWS NAT Gateway. 
2. Discuss why a "Hidden" resource like a NAT Gateway can cost more than the actual servers it is serving. 
3. Propose an alternative (e.g., VPC Endpoints).

**Part 4: Creating a Dashboard**
1. (Conceptual): Design a Grafana dashboard using the "CloudWatch/Billing" data source.
2. Include a "Forecast" line that predicts the bill for the end of the month based on today's spending.
3. Why is "Prediction" more important than "Historical" data?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Tagging is not retroactive. If you add tags to a resource today, you can't see the cost for that tag for last month. Start tagging on Day 1.
- **Gotcha 2:** The "Shared Resource" puzzle. If 10 teams share one massive Kubernetes cluster, how do you split the cost fairly? Research "Kubecost" for cluster cost allocation.

### Reflection Question
How does regular "Cost Visibility" change the way an engineering team writes and deploys code?
