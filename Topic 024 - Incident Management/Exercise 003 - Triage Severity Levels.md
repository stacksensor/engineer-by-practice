# Exercise 003 - Triage & Severity Levels

### Objective
Prioritize under pressure. Learn how to **Triage** incoming issues to determine their **Severity Level** (SEV). Understand how to distinguish between a "Minor Bug" and a "Company-Killing Outage," and learn the different response protocols required for each level of impact.

### Core Concepts to Master
- **Triage:** The process of rapidly evaluating incidents as they arrive.
- **Severity Levels (Common Standards):**
  - **SEV-0/SEV-1 (Critical):** Core service is down for all/most users. Massive revenue loss or data breach. (Immediate "All-Hands-on-Deck" response).
  - **SEV-2 (High):** Major feature is broken for a significant group of users, but the core app still runs.
  - **SEV-3 (Medium):** Minor feature broken, or performance is slow. Impact is localized.
  - **SEV-4 (Low):** UI glitches, typos, or bugs with clear workarounds.
- **Impact vs. Urgency:** 
  - **Impact:** How many people are affected? 
  - **Urgency:** How fast will the damage grow if we don't fix it?

### Research Topics
- "Incident severity level definitions (SEV1, SEV2, SEV3)"
- "How to triage production bugs"
- "Difference between Priority and Severity"

---

### The Practical Challenge

**Part 1: The Triage Desk**
1. Classify these 4 scenarios with a SEV level:
   - Scenario A: A user cannot change their profile picture.
   - Scenario B: The "Pay Now" button is missing for 100% of International users.
   - Scenario C: Every page load takes 30 seconds (standard is 1 second).
   - Scenario D: Admin can see private passwords of all users in the logs.
2. Discuss: Why might Scenario D be a SEV-1 even if "The site is still running perfectly"?

**Part 2: The Timeline of Response**
1. Define the Service Level Objective (SLO) for response times:
   - SEV-1: Response within 5 mins, resolution within 4 hours.
   - SEV-3: Response within 24 hours, resolution within 7 days.
2. Discuss why having these clear rules prevents "Argument-driven development" where every stakeholder thinks their bug is the most important.

**Part 3: Upgrading and Downgrading**
1. You start an incident as a SEV-2 (Searching is slow).
2. During the investigation, the search engine crashes entirely, taking down the Home Page. 
3. Roleplay the process of "Escalating" the incident to a SEV-1. Who needs to be notified?

**Part 4: The Triage Meeting**
1. Research how teams run "Daily Triage" meetings to review new bugs.
2. Discuss why it's important to have both a Product Manager and an Engineer in this meeting.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** SEV-Inflation. If everything is a SEV-1, nothing is a SEV-1. If you cry wolf too many times, engineers will stop treating SEV-1s with the necessary urgency.
- **Gotcha 2:** Only looking at "Volume." A bug affecting 1% of users might be a SEV-1 if that 1% represents the company's biggest "Enterprise" customers who pay 90% of the revenue.

### Reflection Question
How does clear Service Level categorization help prevent "Developer Burnout"?
