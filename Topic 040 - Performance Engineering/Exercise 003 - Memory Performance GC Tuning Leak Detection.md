# Exercise 003 - Memory Performance: GC Tuning & Leak Detection

### Objective
Unclog the RAM. Master **Memory Performance** and the **Garbage Collector (GC)**—the system that automatically frees memory in languages like Python, JS, Java, and Go. Learn how to identify a "Memory Leak," understand why "GC Pauses" cause stuttering in apps and games, and learn how to use a **Heap Dump** to see where the bytes are hiding.

### Core Concepts to Master
- **The Heap:** The pool of RAM where your objects live.
- **The Stack:** Temporary memory for a single function call.
- **Garbage Collector (GC):** The "Cleaner" that finds objects no longer being used and deletes them.
- **GC Pause (Stop the World):** The time when the CPU stops your app to clean the heap. (Bad for games/real-time apps).
- **Memory Leak:** When your code keeps a "Reference" to an object it doesn't need anymore, so the GC can never delete it!
- **Heap Dump:** A "Snapshot" of every object currently in RAM.

### Research Topics
- "How does a Garbage Collector work? (Mark and Sweep)"
- "GC Tuning in Java or Go"
- "Identifying Memory Leaks in Javascript using Chrome DevTools"
- "The concept of 'Generational' GC (Young vs Old gen)"

---

### The Practical Challenge

**Part 1: The "Leaky" Loop (JS)**
1. Write a script: 
   - `let list = []; setInterval(() => list.push(new Array(10000).fill('leak')), 100)`.
2. Open Chrome DevTools -> Performance -> Memory. 
3. Click "Record." Watch the "Heap" memory chart go UP forever.
4. Discuss: Why didn't the GC "Cleanup" this memory? 
5. (Answer: Because the `list` global variable is still "using" every single array).

**Part 2: The Heap Snapshot**
1. Take a "Heap Snapshot" in Chrome DevTools. 
2. Look at the "Summary" tab. 
3. Sort by "Retained Size." 
4. Identify which object is eating all the RAM. 

**Part 3: The "Stop the World" Pain**
1. Research why a **2-second GC pause** is a disaster for a "High-frequency trading" app or a "Multiplayer game." 
2. Discuss: How do you "Tune" the GC to do many small cleans instead of one giant clean? (Hint: Generational collection).

**Part 4: Identifying the leak**
1. Research the **"Closure"** leak in Javascript. 
2. Discuss why a "Hidden" internal function can sometimes keep a "Large parent object" in memory forever just by being alive.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Premature Optimization. Don't worry about "RAM usage" until it actually impacts performance or costs. Having "Free RAM" is a waste of money; using it effectively is the goal!
- **Gotcha 2:** The "Manual" mistake. In C/C++, you have no GC. If you forget to `free()` a single byte, it is gone until the app restarts.

### Reflection Question
Why are "Leak" bugs the hardest type of bug to find in a production application? (Answer: Because they don't cause an immediate crash; they slowly kill the server over several days or weeks).
