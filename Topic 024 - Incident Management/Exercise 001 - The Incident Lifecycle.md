# Exercise 001 - The Incident Lifecycle

### Objective
Master the "Fire Drill." Understand the standard lifecycle of an engineering incident, from the first alert firing to the final resolution. Learn the roles and responsibilities required to handle a production outage without chaos, and understand why "Fixing the system" is only one part of the job.

### Core Concepts to Master
- **The Lifecycle Phases:**
  1. **Detection:** How we find out something is broken (Alerting vs. Customer Report).
  2. **Triage:** Determining the scope and severity of the impact.
  3. **Mitigation:** Stopping the bleeding (e.g., rolling back a deploy or failing over to a backup).
  4. **Resolution:** Fixing the underlying cause.
  5. **Post-Incident:** Learning and preventing the next one.
- **MTTD / MTTR:** 
  - **Mean Time to Detection:** How fast are our alerts?
  - **Mean Time to Resolution:** How fast are our engineers?
- **Incident Commander (IC):** The person who facilitates the response, coordinates communication, and makes the final decisions.

### Research Topics
- "The Google SRE Handbook: Incident Management"
- "Understanding MTTD and MTTR"
- "What is an Incident Commander?"
- "Incident response lifecycle diagram"

---

### The Practical Challenge

**Part 1: The Alert Fired**
1. Imagine it's 3 AM. A PagerDuty alert goes off: "High Error Rate on Checkout API."
2. Flow: 
   - You log in. 
   - You see 100% of purchase attempts are failing.
   - You check the logs. It's a `DatabaseConnectionError`.
3. Discuss: Is your immediate priority to (A) fix the database code or (B) provide a clear status update to stakeholders?

**Part 2: Mitigation vs. Resolution**
1. You discover that a new code deploy 10 minutes ago caused the errors.
2. **Action A (Resolution):** Spend 2 hours debugging and fixing the code.
3. **Action B (Mitigation):** Press "Rollback" to return to the previously working version (takes 2 minutes).
4. Explain why Mitigation is almost always the correct choice for an active SEV-1 incident.

**Part 3: The Dashboard Check**
1. Research how SREs use "Status Dashboards" (like Statuspage.io).
2. Write a sample "Public Update" for a checkout outage that is (a) informative, (b) honest, but (c) doesn't leak sensitive technical details.

**Part 4: Closing the Loop**
1. When the errors stop, the incident isn't "Over."
2. Discuss what steps must be taken immediately after resolution (e.g., closing the ticket, notifying customers, and scheduling the Post-Mortem).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Fixing" by making more changes. In the heat of an incident, engineers often try to "Tweak" production settings. This often makes the situation worse. Rely on documented, tested "Runbooks."
- **Gotcha 2:** The "Missing Stakeholder." If technical teams are fixing the site but nobody told the Support team, they will be overwhelmed by angry customers without any information to give them.

### Reflection Question
Why are "Soft Skills" (Communication, Leadership, Calmness) considered just as important as "Technical Skills" during a major system outage?
