# Exercise 002 - Linear Structures (Stacks & Queues)

### Objective
Master linear data arrays dynamically. Build explicit First-In-First-Out (FIFO) and Last-In-First-Out (LIFO) architectural data structures strictly from raw classes without relying on high-level JavaScript shortcuts.

### Core Concepts to Master
- **LIFO (Stacks):** "Last In, First Out". Operations are strictly limited exactly to `push(data)` and `pop()`. This is exactly how the Browser's "Back" button works.
- **FIFO (Queues):** "First In, First Out". Operations are strictly limited exactly to `enqueue(data)` and `dequeue()`. This is exactly how printer server networks and standard web ticket systems operate.
- **The Call Stack:** The JavaScript Engine's fundamental LIFO stack structurally tracking active function executions natively.

### Research Topics
- "JavaScript implement Stack class"
- "Queues FIFO vs Stacks LIFO"
- "Understanding the JavaScript Call Stack"

---

### The Practical Challenge

**Part 1: The Raw LIFO Stack**
1. In a fresh Node environment, define a pure structural Class `Stack`.
2. Encapsulate a private array: `this.#items = [];`
3. Explicitly construct the interface mathematically. Build `push(element)` to add directly to the array safely.
4. Construct `pop()`. It must actively remove and completely return the final item securely. If the stack is mathematically empty, it must throw a strict algorithmic error: `"Stack Underflow"`.
5. Construct `peek()`. It precisely looks at the final item natively without deleting it.
6. Build a standard `size()` method.

**Part 2: Reversing the Call Stack**
1. Write a function natively `reverseString(string)`.
2. Do not use `.reverse()`. Loop carefully explicitly through the string letters cleanly.
3. `push()` every single character onto an active `Stack` instance you built.
4. Construct an empty output string.
5. While the `Stack.size()` is greater than zero, loop again.
6. Manually `pop()` the characters backwards off the stack and concatenate them together.
7. You structurally demonstrated LIFO behaviors practically and safely.

**Part 3: The FIFO Queue System**
1. Define a strict generic `Queue` class explicitly correctly.
2. Build the exact interface: `enqueue()`, `dequeue()`, `front()`, and `isEmpty()`.
3. You specifically must build testing cases to queue and dequeue print tasks in an array logically.

**Part 4: Real-world Simulation**
1. Write an asynchronous `processQueue()` function safely.
2. Generate 5 random "Document" strings mapping multiple jobs correctly cleanly.
3. Enqueue them realistically.
4. Wait 1 second statically to simulate time passing before pulling the next task dynamically using `dequeue()`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Attempting to use `unshift` instead of `pop` directly massively degrades linear complexity. Building a true queue using a raw Array requires shifting all elements left, which is O(N).
- **Gotcha 2:** Junior developers often confuse exact data ordering structurally. Use queues for network streams securely.

### Reflection Question
Exactly why does JavaScript fundamentally process Call Stack invocations as LIFO explicitly?