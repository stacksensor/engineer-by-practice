# Exercise 005 - Interactive Debugging: Beyond the Print Statement

### Objective
Stop the world. Master **Interactive Debugging**—the art of "Pausing" your code in the middle of a line to see the exact state of every variable. Learn about **Breakpoints**, **Watch Expressions**, **Call Stacks**, and the **browser inspector** (React/Chrome) and understand why "Stepping into" a function is 10x faster than writing "print(x)" 50 times.

### Core Concepts to Master
- **Breakpoint:** A "Red dot" you place on a line of code. The execution will "Pause" exactly there.
- **Variable Inspection:** Seeing `user.id = null` in Real-time without guessing.
- **Call Stack:** The "Map" of every function that was called to get to the current line. (e.g., `main -> auth -> login`).
- **Step Over (F10):** Run the current line and go to the next.
- **Step Into (F11):** Jump inside the function on the current line.
- **Step Out (SHIFT+F11):** Finish the current function and return to the parent.
- **Conditional Breakpoint:** "Only pause if `user_id == 5`."

### Research Topics
- "How to use the VS Code debugger for Node.js or Python"
- "Chrome DevTools: Debugging Javascript with Breakpoints"
- "The Call Stack explained: Finding the source of a bug"
- "Conditional breakpoints: Speed up your debugging"

---

### The Practical Challenge

**Part 1: The "Guessing" Game (Scenario)**
1. You have a bug: `User ID is undefined`.
2. **Standard (Print):** You add `console.log(user)` in 5 different files. You run the app. You look at the logs. You see `null`. You move the log. You repeat 5 times. (Time: 10 minutes).
3. **Debugger:** You place one **Breakpoint** on the login line. You run the app. It pauses. You hover your mouse over `user`. You see `id: undefined`. 
4. Discuss: How much faster was the **Debugger**? (Answer: 2 minutes vs 10 minutes).

**Part 2: The "Traceback" (Call Stack)**
1. Research how to read a **Call Stack** in Chrome DevTools. 
2. Discuss: If you see a "Crash" in a third-party library, how do you find which line of YOUR code called that library? 
3. (Answer: By clicking the 2nd or 3rd item in the Call Stack).

**Part 3: The "Wait" state**
1. Research the **`debugger;`** statement in Javascript. 
2. Discuss why putting this in your code is a "Forced Breakpoint" that works in any browser.

**Part 4: Identifying the command**
1. Research the **Step Over** vs **Step Into** shortcuts in VS Code. 
2. When should you choose **Into**? (Answer: When you think the bug is INSIDE the function you are about to call).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Async" trap. Debugging code that uses `setTimeout` or `Promises` is hard because the "Call Stack" might look different than you expect. (Tip: Use "Async Stack Traces" in Chrome).
- **Gotcha 2:** Production "Minification." If you try to debug a "Live" site where the code is scrambled (`a.b(c)`), it will be impossible. (Solution: See Topic 042: Source Maps!).

### Reflection Question
Why are "Print" statements still popular despite "Debuggers" being more powerful? (Answer: Because they are "Universal" and work even on servers where you can't attach a debugger).
