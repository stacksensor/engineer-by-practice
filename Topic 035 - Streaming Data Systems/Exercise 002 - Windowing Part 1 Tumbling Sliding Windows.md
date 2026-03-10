# Exercise 002 - Windowing Part 1: Tumbling & Sliding

### Objective
Slice the timeline. Master the concept of **Windowing**—the way we perform "Aggregations" (like Sum, Average, or Count) on an infinite stream of data. Learn the difference between **Tumbling Windows** (Fix-sized, non-overlapping) and **Sliding Windows** (Overlapping) and understand which to use for "Hourly Totals" vs "Running Averages."

### Core Concepts to Master
- **The Window:** A logical "bucket" of time (or record count) used to group data.
- **Tumbling Window:** Fixed intervals (e.g., 00:00-00:10, 00:10-00:20). A message belongs to exactly ONE window.
- **Sliding Window:** Overlapping intervals (e.g., "A 1-minute window that starts every 10 seconds"). A message can belong to MULTIPLE windows.
- **Trigger:** The signal that causes the window to "Fire" and output its result (usually just the end of the time period).

### Research Topics
- "Types of Windows in Stream Processing (Flink/Spark)"
- "Tumbling vs Sliding Windows: A visual guide"
- "Applying a Sliding Window for a 24-hour moving average"
- "The cost of overlapping windows"

---

### The Practical Challenge

**Part 1: The Tumbling Count**
1. Data arrives: `[00:01]: 5`, `[00:05]: 10`, `[00:12]: 2`.
2. Windows: Every 10 minutes.
3. Calculate the sum for Window 1 (00:00-00:10) and Window 2 (00:10-00:20).
4. (Answer: W1 = 15, W2 = 2).

**Part 2: The Sliding Average**
1. Window size: 60 seconds. Slide: 30 seconds.
2. An event arrives at `00:45`.
3. Which windows does it belong to?
   - Window A: `00:00 - 01:00`.
   - Window B: `00:30 - 01:30`.
4. Discuss: Why is this better for a "Stock Price" charts than a Tumbling window? (Answer: It provides a "Smooth" line rather than a "Jump" every minute).

**Part 3: The "Hop" tradeoff**
1. Research what a **Hopping Window** (another name for Sliding) is. 
2. Discuss: If your window is 1 hour but your "Slide" is 1 millisecond, what happens to your computer? (Answer: It explodes trying to manage 3,600,000 active windows for every message).

**Part 4: Identifying the window**
1. Which window for:
   - "How many people visited the site in the last 10 minutes?" (Every 10 min). (Answer: Tumbling).
   - "Detecting a 10% spike in errors over any 5-minute period." (Answer: Sliding).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Processing Time vs Event Time. What if a message from 1:59 arrives at 2:01? Does it go in the old window or the new one? (Answer: This depends on your "Watermarking" strategy).
- **Gotcha 2:** Window "Lateness." If you wait 24 hours for "late data" before closing a window, your dashboard will be 24 hours out of date!

### Reflection Question
Why are windows necessary in stream processing but not in standard SQL queries? (Answer: Because you can't "Aggregate" an infinite total—you must define a boundary).
