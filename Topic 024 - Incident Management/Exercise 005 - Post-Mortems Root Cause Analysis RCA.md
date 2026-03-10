# Exercise 005 - Post-Mortems & Root Cause Analysis (RCA)

### Objective
Turn failures into features. Learn how to conduct a **Post-Mortem** (Incident Review). Master **Root Cause Analysis (RCA)** using techniques like the **"5 Whys"** to move beyond "Human Error" and identify the systemic weaknesses that allowed the incident to happen.

### Core Concepts to Master
- **The Post-Mortem Document:** A formal report containing the incident timeline, impact, root cause, and follow-up actions.
- **The 5 Whys:** A technique of asking "Why" five times to drill down through symptoms to the physical/process root cause.
- **Root Cause vs. Contributing Factors:** Understanding that complex failures almost never have a single "Root" cause, but are a chain of multiple small failures.
- **Action Items:** Specific, trackable tickets (Jira/GitHub) created to ensure the same incident never happens again.

### Research Topics
- "How to write a blameless post-mortem"
- "The 5 Whys root cause analysis examples"
- "Google's post-mortem template"

---

### The Practical Challenge

**Part 1: The "5 Whys" in Action**
1. Incident: The website went down for 2 hours.
   - Why 1? The database ran out of disk space.
   - Why 2? Log files were not being deleted.
   - Why 3? The log-rotation script failed.
   - Why 4? The disk was full so the script couldn't write its own lock file.
   - Why 5? We didn't have an alert for disk usage > 80%.
2. Identify the true Root Cause. Is it "The full disk" or "The missing alert"?

**Part 2: The Timeline Reconstruction**
1. Collect "Artifacts" from a hypothetical incident (Slack screenshots, Grafana links, GitHub commit IDs).
2. Create a chronological timeline:
   - 12:00: Bad code merged.
   - 12:05: Errors start rising.
   - 12:15: Pager fires.
   - 12:20: Engineer starts investigating.
3. Discuss: Where was the biggest delay? Detection or Mitigation?

**Part 3: Documenting the "Lessons Learned"**
1. Write a section for a Post-Mortem titled "What went well" and "What went poorly."
2. Even in a disaster, things can go well (e.g., "The rollback was fast," "The communication team was proactive").

**Part 4: Assigning Action Items**
1. Don't just say "We will be more careful."
2. Write 3 actionable items:
   - "Add Prometheus alert for DiskSpace < 20%."
   - "Automate log rotation testing in CI."
   - "Move database logs to a separate physical volume."

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Human Error" as a Root Cause. If your conclusion is "Bob made a mistake," you have failed the RCA. The real question is: "Why was Bob *allowed* to make a mistake that took down the whole site?" (e.g., Missing safeguards/tests).
- **Gotcha 2:** The "Bottom of the Drawer." Many teams write great Post-Mortems but then never do the follow-up work. Action items must be prioritized like any other feature.

### Reflection Question
Why is a Post-Mortem useless if it doesn't result in a change to the code or the process?
