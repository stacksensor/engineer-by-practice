# Exercise 004 - Commitments (Savings Plans & Reserved Instances)

### Objective
Commit to save. Master the "Discount" models of the cloud. Learn how to use **Reserved Instances (RIs)** and **Savings Plans** to get 30%-70% discounts on your cloud spend in exchange for committing to use a certain amount of compute over 1 or 3 years.

### Core Concepts to Master
- **On-Demand Pricing:** Paying the "Retail" price for maximum flexibility (no commitment).
- **Reserved Instances (RI):** Committing to a specific instance type/size in a specific region.
- **Savings Plans:** A more flexible commitment where you commit to a dollar-per-hour spend (e.g., "$10/hour") across any instance size.
- **Pay Upfront vs. No Upfront:** The trade-off between cash flow and higher discounts.

### Research Topics
- "AWS Savings Plans vs Reserved Instances: Which to choose?"
- "GCP Committed Use Discounts (CUD)"
- "Calculating the ROI of a 3-year No-Upfront Savings Plan"

---

### The Practical Challenge

**Part 1: The "On-Demand" Penalty**
1. You are running a website that consistently uses 10 servers 24/7.
2. Price A (On-demand): $1000/month.
3. Price B (Savings Plan): $600/month (with a 1-year contract).
4. Discuss: Why would anyone *ever* choose Price A? (Hint: Flexible scaling/testing).

**Part 2: Planning the Commitment**
1. Look at your historical cloud usage for the last 6 months.
2. If your "Minimum" usage never dropped below $5/hour, but your "Peak" was $20/hour, how much should you commit to in a Savings Plan? (Answer: Close to $5/hour, the "Baseload").
3. Discuss the risk of "Over-committing": What happens if your company pivots and stops using that cloud provider next month?

**Part 3: Upfront vs. Monthly**
1. Research the discount levels for:
   - "All Upfront" (Pay $10k now).
   - "Partial Upfront."
   - "No Upfront" (Pay monthly but at a fixed rate).
2. Discuss why a "Finance Director" cares more about this choice than an "Engineering Lead."

**Part 4: Managing Expirations**
1. Research what happens when a 1-year RI expires without you noticing. 
2. (Hint: Your bill instantly jumps by 40%).
3. How would you automate an alert to warn the team 30 days before a contract expires?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** RI Lock-in. Traditional RIs were often locked to a specific "Size" (e.g., m5.large). If you wanted to upgrade to m6.large, your RI was useless. Modern Savings Plans and "Convertible RIs" solve this.
- **Gotcha 2:** The "Unused Commitment." If you commit to $10/hour but only use $8/hour, you still pay for $10. You are "wasting" $2/hour on air.

### Reflection Question
How do Savings Plans represent a "Contract between Engineering and Finance"?
