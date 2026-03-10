# Exercise 003 - Windowing Part 2: Session & Global

### Objective
Group by activity, not just time. Master advanced windowing techniques: **Session Windows** (Defined by gaps in activity) and **Global Windows** (Infinite windows that use custom triggers). Learn how to track "User Sessions" where one user might stay on the site for 5 minutes and another for 2 hours.

### Core Concepts to Master
- **Session Window:** A window that starts when a user arrives and "Timed out" after a period of inactivity (e.g., 30 minutes of no clicks).
- **Gap Duration:** The "Inactivity" time used to decide when a session ends.
- **Global Window:** A single window that contains all data from the beginning of time. It only outputs data when a specific "Trigger" occurs (e.g., "Every 1,000 units").
- **Stateful Processing:** How the streaming engine "Remembers" a user's activity across multiple messages.

### Research Topics
- "How Session Windows work in Apache Flink"
- "Triggering logic in Global Windows"
- "Sessionization: Grouping clicks into a single visit"
- "The difference between Time-based and Count-based windows"

---

### The Practical Challenge

**Part 1: The Visit Tracker**
1. User clicks at: `12:00`, `12:05`, `12:10`. 
2. Session gap: 15 minutes.
3. Does this count as one session or two? (Answer: One, because the gap between clicks is always <15m).
4. User clicks again at `12:30`.
5. Now how many sessions are there? (Answer: Two. The gap between 12:10 and 12:30 was 20m, exceeding the 15m limit).

**Part 2: The Global Count**
1. You want to send an alert every time you sell 1,000 items, regardless of how long it takes.
2. Discuss why a "Tumbling Window" (Time-based) is the wrong tool for this. 
3. (Answer: If you sell 1,000 items in 1 minute, you want the alert NOW, not at the end of a 10-minute window).
4. Research the "Count Trigger" for Global Windows.

**Part 3: The Merging Problem**
1. Research what happens in a Session Window if data arrives out of order.
2. Event A (`12:00`) and Event C (`12:30`) arrive first. (The engine creates 2 sessions).
3. Then Event B (`12:15`) arrives. 
4. How does the engine "Merge" the two sessions into one?

**Part 4: Identifying the window**
1. Which window for:
   - "Measuring the bounce rate of users" (Answer: Session).
   - "A 24-hour leaderboard that resets at midnight" (Answer: Global with a midnight trigger).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Memory Leak. If you use a Session Window with a 1,000-year timeout, the streaming engine will try to keep millions of user sessions in RAM forever.
- **Gotcha 2:** Late Arrival. If a user click from "yesterday" arrive today, does it reopen their old session? (Answer: Only if your "Allowed Lateness" configuration allows it).

### Reflection Question
Why are Session Windows considered "Data-driven" while Tumbling/Sliding windows are "Time-driven"? (Answer: Because session boundaries are defined by the user's behavior, not the clock).
