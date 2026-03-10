# Exercise 005 - Async I (Event Loop & Callbacks)

### Objective
Break out of linear, top-to-bottom procedural execution. Master JavaScript's non-blocking, asynchronous architecture where scheduled tasks execute seamlessly outside of the primary UI thread while the main script continues onward.

### Core Concepts to Master
- **The Call Stack:** The single-threaded physical execution queue. JS executes one function exclusively at a time.
- **The Web APIs (Browser):** Functions like `setTimeout` or `fetch` are NOT physically executed by Javascript natively! JS hands them off to the Browser's C++ threads entirely.
- **The Event Queue & Event Loop:** The endless spinning cycle that checks if the Call Stack is completely empty, and if so, physically pushes waiting Background Web API tasks back into the primary Stack to continue executing.
- **Callback Functions (Again):** A function passed as a strict payload algorithm to executed precisely when the Web API definitively finishes its task.

### Research Topics
- "What the heck is the event loop Philip Roberts (YouTube)" -> *MANDATORY WATCH*
- "JavaScript Call Stack explained"
- "Synchronous vs Asynchronous code Execution"

---

### The Practical Challenge

**Part 1: The Illusion of Time**
1. Create `async.js` and write three simple linear console logs:
   ```javascript
   console.log("1. Start");
   setTimeout(() => { console.log("2. Timer Finished"); }, 0);
   console.log("3. End");
   ```
2. Look strictly at the timeout delay. It is set mathematically to `0` milliseconds.
3. Guess the physical console output order, then run `node async.js`.
4. It outputs `1`, then `3`, then `2`! WHY? 
5. Understand the path:
   - JS puts '1' on the stack and instantly executes it.
   - JS sees `setTimeout`. It passes the physical callback function entirely off to the Browser/Node Background Web API and immediately deletes `setTimeout` from the primary stack.
   - JS moves onward to '3' and executes it. 
   - Meanwhile, the Web API waited 0 milliseconds, and dropped the Callback function into the Task Queue.
   - The Event Loop verifies the main stack is finally fully empty, grabs the Callback, pushes it onto the main stack, and JS physically logs '2'.

**Part 2: The Blocking UI Trap**
1. Open a raw HTML file template with a gigantic clickable `<button>Click</button>`.
2. Add an inline physics-crashing Synchronous while-loop before a console log:
   ```javascript
   function blockEverything() {
       let i = 0;
       while (i < 5000000000) { i++; } // 5 Billion Iterations
       console.log("Loop finished");
   }
   blockEverything();
   console.log("App ready");
   ```
3. Load the HTML file. Frantically try clicking the button, highlighting text on the screen, or scrolling. The entire browser tab is seemingly frozen and physically dead.
4. Eventually, "Loop finished" and "App ready" log heavily. The UI magically unlocks.
5. *Lesson:* Because the JS Call Stack is purely Single-Threaded, if a massive mathematical operation (like image processing) is forced synchronously directly onto the main stack, it entirely blocks the browser from physically rendering physical UI animations or processing user mouse clicks for seconds.

**Part 3: The Nightmare "Callback Hell"**
1. Write a script simulating logging into a mocked database over a slow fake 1-second network connection:
   ```javascript
   function loginUser(email, password, callback) {
       setTimeout(() => { 
           console.log("Data received over network"); 
           callback({ email: email }); 
       }, 1000);
   }
   ```
2. Trigger it: `let user = loginUser("test@test", "123");`. Notice that `user` is horrifyingly `undefined`, because `loginUser` lacked a physical return statement (it finishes in the background seconds later).
3. Connect a callback logic algorithm:
   ```javascript
   loginUser("test", "pwd", (userObj) => {
       console.log(userObj.email);
   });
   ```
4. Now, imagine needing to take that simulated `userObj`, and trigger a second async server function to `getPosts(userObj.email)`. You have to nest a new callback physically inside the first callback. 
5. Then nest `getComments(post)`. Notice the physical text cursor drifting radically to the right side of the screen into the notorious "Pyramid of Doom".

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** A `setTimeout(() => {}, 2000)` does **NOT** guarantee execution in exactly 2000 milliseconds. It mathematically guarantees it will wait a minimum of 2000 milliseconds, but if the main Call Stack is backlogged with a massive synchronous `while` loop, the timeout must sit stuck trapped in the Event Queue queue indefinitely.
- **Gotcha 2:** It is physically impossible to export or natively `return` a calculated value securely out of a standard async Callback block straight back to the global synchronous file scope. The global logic continues moving onward down the page long before the callback is structurally resolved in RAM.

### Reflection Question
If JavaScript operates purely linearly on a single physical thread core (unlike multi-core threaded languages like Java or C#), how can it mathematically handle 10,000 massively heavy network API requests originating simultaneously without instantly freezing up?