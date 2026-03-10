# Exercise 002 - On-Call Preparedness & PagerDuty

### Objective
Be ready when the phone rings. Learn the operational "Hard Work" of being **On-Call**. Understand how to set up escalation policies, handle "Alert Fatigue" by tuning your thresholds, and how to create effective **Runbooks** so that any engineer can fix a problem they didn't create.

### Core Concepts to Master
- **On-Call Rotation:** A schedule ensuring that at least one engineer is always available for emergencies.
- **Escalation Policy:** If the first person doesn't answer within 5 minutes, the alert "Escalates" to the second person (and eventually to the manager).
- **Runbook / Playbook:** A step-by-step document that explains how to diagnose and fix a specific alert (e.g., "What to do when Redis memory exceeds 90%").
- **Alert Fatigue:** The dangerous state where an engineer starts ignoring alerts because the system sends too many "False Alarms" (e.g., CPU spikes that don't actually break anything).

### Research Topics
- "Best practices for engineering on-call rotations"
- "How to write a good runbook"
- "PagerDuty escalation policy patterns"
- "Reducing alert noise in Prometheus/Grafana"

---

### The Practical Challenge

**Part 1: The Escalation Logic**
1. Design an escalation policy for a team of 4 engineers.
2. Tier 1: Primary On-call (15 mins to respond).
3. Tier 2: Secondary / Shadow On-call.
4. Tier 3: Engineering Manager.
5. Discuss: Why is it important to have a "Secondary" person even if the Primary is very reliable?

**Part 2: Designing a Runbook**
1. Create a "Runbook Template" with sections for:
   - **Alert Title:** "High Latency on API Gateway".
   - **Description:** What does this alert actually mean?
   - **Diagnosis:** Which dashboard should I look at? What queries should I run?
   - **Mitigation:** How do I make it stop immediately?
   - **Escalation:** Who do I call if I can't fix it? (e.g., The Database Team).

**Part 3: Tuning for Sanity**
1. Imagine an alert: "CPU Usage > 80% for 1 minute."
2. This alert fires every day at 12 PM when the "Backup Job" runs, but the site remains fast.
3. Discuss: How would you "Tune" this alert to stop waking you up? (e.g., Move threshold to 95%, or change the duration to 15 minutes).

**Part 4: The Handover**
1. When your week of on-call is over, how do you communicate with the next person?
2. Create a "Handover Checklist" (e.g., List of alerts that fired, unresolved bugs, system changes).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Actionable" Alerts. If an alert tells you something is wrong but there is literally nothing you can do about it, that alert should be a "Warning" in a dashboard, NOT a page to your phone.
- **Gotcha 2:** Outdated Runbooks. A runbook from 2021 that tells you to restart a server that was deleted in 2023 is worse than no runbook at all. Make runbook updates part of your Post-Mortem process.

### Reflection Question
How does a well-documented on-call culture reduce developer "Burnout" and improve the team's mental health?
