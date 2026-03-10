# Exercise 004 - Effective Communication during Outages

### Objective
Maintain trust when things break. Learn how to communicate effectively during a high-pressure incident. Master the art of **Status Updates**—both internal (to bosses and other teams) and external (to customers)—ensuring that everyone is informed, anxiety is reduced, and the technical team is protected from constant interruptions.

### Core Concepts to Master
- **The "Single Source of Truth":** Having a dedicated Slack channel or document where all updates are posted.
- **Internal Synchronous Updates:** The "War Room" or incident bridge (Zoom/Call).
- **Stakeholder Updates:** Regular "Pulse" messages (e.g., every 30 mins) even if there is no new technical progress.
- **Tone & Transparency:** Being honest about the failure without over-sharing raw technical jargon that could be misinterpreted or leak security info.
- **The "Incident Liaison":** A role dedicated to translating technical updates into business language for non-technical leadership.

### Research Topics
- "Crisis communication for engineers"
- "How to write a public status update"
- "Slack etiquette during production incidents"

---

### The Practical Challenge

**Part 1: The Internal Status Update**
1. Write an update for an internal Slack channel (#incidents) for a SEV-1.
2. It MUST include:
   - **Current Status:** (Investigating / Mitigating / Monitoring).
   - **Impact:** What is broken and for whom?
   - **What we are doing now:** Who is working on what?
   - **ETA for next update:** "Next update in 20 minutes."

**Part 2: The "Boss" Translation**
1. Technical Update: "Our Redis primary node is flapping due to OOM constraints causing a sequence of failovers to a stale replica."
2. Write a translation of this for the CEO who is asking "Why is the site down?".
3. (Hint: Focus on the *user experience* and the *path to fix*, not the Redis log messages).

**Part 3: Managing the "Loudroom"**
1. Imagine 50 people join your incident Slack channel and everyone starts asking "When will it be fixed?".
2. Research how to use Slack's **Channel Canvas** or a **Pinned Message** to prevent repetitive questions.
3. Roleplay as the "Incident Commander" telling a curious VP to "Please stay off the thread to let the engineers focus."

**Part 4: The Public Status Page**
1. Go to `status.github.com` or `status.twitter.com` (if available). 
2. Look at an archived incident.
3. Compare the "Initial Report" to the "Resolved Report." Note the change in tone and detail.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Silence is Panic. If an hour passes without an update, stakeholders will assume you have lost control of the system. Even "We are still debugging the database" is a valuable update.
- **Gotcha 2:** Promising a fixed Time. Never say "It will be back in 5 minutes" unless you have already pressed the button and are watching the green lights. Always use ranges or say "We are working toward mitigation."

### Reflection Question
Why is "Over-communicating" better than "Under-communicating" during the first 30 minutes of a major outage?
