# Exercise 002 - CPU Performance: Profiling & Flame Graphs

### Objective
See where the time goes. Master **CPU Profiling**—the technique of measuring how much time your code spends in each function. Learn about **Sampling Profilers**, **Instruction Counting**, and the **Flame Graph**—the industry-standard visualization for finding the "Hot" path in your code.

### Core Concepts to Master
- **Profiling:** Measuring an application's performance as it runs.
- **Flame Graph:** A visualization where the "X" axis is the population (width = time spent) and "Y" axis is the stack depth.
- **Cold vs Warm functions:** "Hot" functions are executed millions of times; "Cold" once. 
- **Sampling profiler:** Checking the CPU every 1 millisecond to see which function is running (Low overhead).
- **Instrumentation profiler:** Adding a "Timer" to every single function call (Highest precision, very slow).

### Research Topics
- "What is a Flame Graph? (Brendan Gregg's guide)"
- "Using the Chrome DevTools 'Performance' tab"
- "Python Profiling with 'cProfile' or 'py-spy'"
- "Identifying CPU bottlenecks in internal code"

---

### The Practical Challenge

**Part 1: The Chrome Flame Graph**
1. Open a complex website (like Twitter/X or a heavy news site).
2. Open DevTools -> Performance tab. 
3. Click "Record" and refresh the page.
4. Look at the "Main" flame graph. 
5. Find the "Widest" rectangle. Which function is it? (Answer: Usually something like `Recalculate Style` or a large Javascript library).

**Part 2: The Loop Trap (Python)**
1. Write two functions:
   - `func_a()`: Does 10 calculations.
   - `func_b()`: Calls `func_a()` inside a loop of 1,000,000.
2. Run a profiler (like `cProfile` in Python).
3. Observe the output. Which function shows the "Total Time"? 
4. (Answer: `func_b` might be the "Root," but `func_a` is where the CPU is actually working).

**Part 3: The "Wait" state**
1. Research how a "Network call" looks on a flame graph. 
2. (Answer: It often looks like a "Gap" or a "Wait" state where the CPU is doing nothing).
3. Discuss why you shouldn't "Optimize the CPU" if the bottleneck is a 2-second database query.

**Part 4: Identifying the "Hot" path**
1. Research the **"80/20 Rule"** in performance. 
2. Why is it better to optimize 1 line of code that runs 1,000,000 times than it is to optimize 1,000 lines of code that run once?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Profiling in "Debug" mode. If you profile your code in debug mode, the results will be 10x slower and completely different from "Production" mode where the compiler uses optimizations.
- **Gotcha 2:** The "Heisenbug." Sometimes adding a profiler makes the app so slow that a "Race condition" bug disappears.

### Reflection Question
Why are "Flame Graphs" shaped like mountains or flames instead of simple bar charts? (Answer: Because they show the "Hierarchy" of function calls, with parents at the bottom and children at the top).
