# Exercise 006 - Interrupts & Exceptions

### Objective
Drop everything. Master how the CPU handles unexpected events. Learn about **Hardware Interrupts** (asynchronous events from mouse, keyboard, or network) and **Software Exceptions** (synchronous events like "Dividing by Zero" or "Segmentation Fault"). Understand the **Interrupt Vector Table (IVT)**.

### Core Concepts to Master
- **Interrupt:** A signal from hardware or software indicating an event that needs immediate attention.
- **Exception:** A special case of interrupt triggered by the executing instruction (e.g., invalid math).
- **Asynchronous vs. Synchronous:** Interrupts happen "anytime"; Exceptions happen "right now" because of your code.
- **ISR (Interrupt Service Routine):** The specific code in the Kernel that runs when an interrupt occurs.

### Research Topics
- "How do hardware interrupts work?"
- "The difference between an Interrupt and an Exception"
- "Maskable vs Non-maskable interrupts (NMI)"
- "Top Half vs Bottom Half execution in the Linux Kernel"

---

### The Practical Challenge

**Part 1: The Mouse Handler (Hardware)**
1. Every time you move your mouse, a hardware interrupt is sent to the CPU. 
2. Research: If you move your mouse 1,000 times a second, why doesn't your computer freeze? (Hint: The "Top Half" handler is extremely fast).

**Part 2: The Crash (Software Exception)**
1. Write a line of code in Python/C: `print(1/0)`. 
2. Observe the error. Discuss: How did the CPU know you divided by zero? (Answer: The math unit triggered an exception interrupt).
3. Research what a "Segmentation Fault" is in C. Which part of hardware detected it? (Answer: The MMU).

**Part 3: The Interrupt Vector Table (IVT)**
1. Research the IVT. It's an array of "Pointers to functions." 
2. Entry #0 is usually "Divide by Zero." Entry #14 is "Page Fault."
3. Discuss: If a virus changes the pointer for "Keyboard" to its own code, what happens when you type your password?

**Part 4: The Mode Switch**
1. Explain why every single interrupt forces the CPU to switch from "User Mode" to "Kernel Mode." 
2. (Answer: Only the Kernel is allowed to touch hardware or fix a page fault).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Interrupt Storm. If a piece of hardware is broken and sends 1,000,000 interrupts a second, the CPU will spend 100% of its time running the "Handler" and nothing else.
- **Gotcha 2:** Disabling Interrupts. Kernels sometimes "Mask" (turn off) interrupts so they can finish a sensitive task. If they forget to turn them back on, the keyboard and mouse stop working!

### Reflection Question
Why are "Interrupts" essential for making your computer feel "Responsive" and "Real-time"?
