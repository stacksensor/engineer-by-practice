# Exercise 007 - The "FinOps" Post-Mortem & Reporting

### Objective
Close the loop. Learn how to conduct a "Cost Post-Mortem" after a major billing deviation. Master the art of reporting "Cost Savings" and "Efficiency Gains" to leadership, ensuring that the engineering team's efforts to reduce cloud spend are recognized and valued by the business.

### Core Concepts to Master
- **Billing Anomalies:** When the daily spend suddenly doubles or drops for an unknown reason.
- **Attribution Reporting:** Showing a chart of "Service A costs $X" vs "Service B costs $Y."
- **Efficiency Metrics:** Moving from "Total Cost" to "Cost per Business Metric" (e.g., Cost per Transaction).
- **The Savings Log:** Keeping a historical record of every optimization (e.g., "Right-sized RDS, saved $2k/month").

### Research Topics
- "Communicating cloud savings to executives"
- "Cost anomaly detection tools (AWS Cost Anomaly Detection)"
- "Defining engineering KPIs for cloud efficiency"

---

### The Practical Challenge

**Part 1: Investigating the Anomaly**
1. You receive an alert: "Daily S3 spend grew by 400% in 24 hours."
2. Triage the cause: 
   - Is it higher traffic? (Legitimate).
   - Is it a bug in the cleanup script? (Technical debt).
   - Is it someone testing a migration? (Process failure).
3. Write a short update for the Finance team explaining the spike and the path to fix.

**Part 2: The "Efficiency" Chart**
1. Imagine your company's traffic doubled. Your cloud bill also doubled.
2. Discuss: Is this a success or a failure? (Answer: Neutral. Efficiency is flat).
3. Imagine traffic doubled but your cloud bill only grew by 10%.
4. Explain how this "Decrease in Cost per User" is the ultimate proof of a high-performing engineering team.

**Part 3: The "FinOps" Meeting**
1. Design a 15-minute monthly meeting structure between Engineering, Finance, and Product.
2. Agenda:
   - Review last month's invoice.
   - Review 3 biggest cost drivers.
   - Propose 1 "Optimization project" for the next sprint.

**Part 4: The Impact Report**
1. You spent 2 days right-sizing servers and saved the company $2,000 / month ($24,000 / year).
2. Write a celebratory email to the VP of Engineering: 
   - "How much was saved."
   - "How little work it took (ROI)."
   - "What other optimization we found for next time."

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Discounting "Human Time." If you spend $50,000 in developer salaries to save $50 / month on AWS, you have failed the math. Always include the "Cost of Engineering" in your calculations.
- **Gotcha 2:** The Rebate/Credit Trap. Sometimes cloud providers give you "Free Credits." Don't let these mask an inefficient architecture. Eventually, the credits run out!

### Reflection Question
How does regular "Cost Reporting" help engineering teams get more "Budget" for the technical projects they care about?
