# Exercise 001 - Introduction to FinOps

### Objective
Master the business of cloud. Learn the principles of **FinOps** (Cloud Financial Operations)—the practice of bringing financial accountability to the variable spend model of the cloud. Understand why "Cloud Economics" is a required skill for senior engineers and how to balance **Speed**, **Cost**, and **Quality**.

### Core Concepts to Master
- **The FinOps Lifecycle:** Inform (Visibility) -> Optimize (Action) -> Operate (Continuous).
- **Variable Spend Model:** How cloud differs from traditional "Data Centers" (Capex vs Opex).
- **The Triangle of Trade-offs:** Speed of development vs. Cost of infrastructure vs. Reliability/Performance.
- **Unit Economics:** Calculating the "Cost per Transaction" or "Cost per Active User."

### Research Topics
- "What is FinOps? (FinOps Foundation)"
- "The 6 Principles of FinOps"
- "Cloud Economics 101: Understanding OpEx"
- "Unit Economics for software engineers"

---

### The Practical Challenge

**Part 1: The Sticker Shock (Case Study)**
1. Research a story where a company accidentally left a massive cloud resource running (e.g., the $72,000 Firebase bill story).
2. Discuss: Why did this happen? (e.g., Infinite loop, missing alerts, unintended scale).
3. How would a "FinOps mindset" have prevented this?

**Part 2: Calculating Unit Economics**
1. Imagine an app with:
   - $10,000 monthly AWS bill.
   - 100,000 active users.
   - 1,000,000 total database queries per month.
2. Calculate:
   - Cost per User per month.
   - Cost per 1,000 Queries.
3. If the Marketing team brings in 1,000,000 new users, what will your bill be next month?

**Part 3: Capex vs. Opex**
1. Research the difference between Capital Expenditure (Buying servers upfront) and Operating Expenditure (Paying for what you use).
2. Discuss: Why does a startup prefer Opex, but a massive company like Facebook prefers Capex (building their own data centers)?

**Part 4: Setting a Budget Alert**
1. (Conceptual or Lab): Research how to set a "Budget Alert" in AWS, GCP, or Azure.
2. Define a policy: "If my monthly spend hits 80% of $5,000, send me a Slack message."
3. Why is "Detection" better than "Constraint" (e.g., why don't we just hard-limit the budget and shut the site down when it runs out)?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Shadow IT" problem. Engineers often spin up "Test" clusters and forget to delete them. This accounts for a significant % of wasted cloud spend.
- **Gotcha 2:** Only focusing on savings. FinOps is not about "Saving money" at all costs; it's about "Making money efficiently." Spending $1k to make $10k is a success!

### Reflection Question
Why is a Senior Engineer who understands "The Bill" often more valuable to a company than one who only understands "The Code"?
