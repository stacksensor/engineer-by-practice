# Exercise 006 - Async II (Promises & Async/Await)

### Objective
Destroy the messy indentation of Callback Hell. Harness the modern structural power of native Promises and the syntactic magic of `async/await` to force asynchronous background tasks to read perfectly like flat, linear, synchronous code.

### Core Concepts to Master
- **The Promise Object:** A structural placeholder object directly representing the eventual completion (or fatal failure) of a background asynchronous operation and its resulting data.
- **Promise States:** `Pending` -> Resolves cleanly (`Fulfilled`) or Crashes violently (`Rejected`).
- **`.then() / .catch()`:** Native chainable methods to execute subsequent functions securely after a Promise strictly fulfills or rejects.
- **`async / await`:** Modern ES8 sugar that physically halts the visual execution of your function block securely *until* a Promise strictly finishes, without brutally blocking the main structural JavaScript UI thread.

### Research Topics
- "JavaScript Promises explained then catch"
- "How does async await work logically in JS"
- "JavaScript fetch API example Promises"
- "Promise.all for parallel network requests"

---

### The Practical Challenge

**Part 1: Constructing the Physical Promise**
1. Replace yesterday's painful Callback design. Create a native Promise that physically flips a coin.
   ```javascript
   const flipCoin = new Promise((resolve, reject) => {
       console.log("Minting coin (simulated network request)...");
       setTimeout(() => {
           const isHeads = Math.random() > 0.5;
           if (isHeads) { resolve("Winner! It was Heads!"); }
           else { reject("Fatal Error: It was Tails."); }
       }, 1500);
   });
   ```
2. Log `flipCoin` immediately on the next line: `console.log(flipCoin);`. You will see `Promise { <pending> }`. The coin is currently flipping physically in the air.
3. Delete the log. Consume the result securely using chained methods:
   ```javascript
   flipCoin
      .then(resultString => console.log("Success:", resultString))
      .catch(errorString => console.error("Failed:", errorString));
   console.log("Code executed perfectly and moved on immediately.");
   ```

**Part 2: The Network `fetch` API**
1. Open the browser console or use a NodeJS version `18+` environment.
2. We are going to ping a real physical server using the native `fetch()` browser API (which mathematically returns a Promise by default).
3. Build the payload chain:
   ```javascript
   fetch("https://jsonplaceholder.typicode.com/users/1")
      .then(response => {
           // We have the raw network packet! Now we parse the physical JSON string body, 
           // which incredibly, returns a SECOND nested Promise!
           return response.json(); 
      })
      .then(userObject => {
           console.log("Target Acquired:", userObject.name);
      })
      .catch(err => {
           console.log("The physical network cable is broken.", err);
      });
   ```

**Part 3: The `async / await` Magic**
1. The `.then()` chaining above is infinitely cleaner than Callback Hell, but it still requires messy nested arrow functions. 
2. Rewrite the exact same `fetch` logic using ES8 linear Syntax:
   ```javascript
   async function getTargetData() {
       try {
           // Await physically pauses this specific function block until the network packet hits.
           const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
           const userObject = await response.json();
           console.log("Target Acquired (Async):", userObject.name);
       } catch (err) {
           console.log("Caught Error:", err);
       }
   }
   getTargetData();
   ```
3. Look at the code. It literally reads like completely flat synchronous blocking code! The `try/catch` securely handles the Promise rejections without specific `.catch()` chains.

**Part 4: Parallel Processing Execution**
1. Imagine grabbing User 1, User 2, and User 3 sequentially:
   ```javascript
   const res1 = await fetch(".../users/1");
   const res2 = await fetch(".../users/2");
   const res3 = await fetch(".../users/3");
   ```
2. This is historically called a "Waterfall" bottleneck. If each request securely takes `1 second`, the user waits **3 seconds total**.
3. Fire them simultaneously into the background using `Promise.all`:
   ```javascript
   const endpoints = [fetch("URL1"), fetch("URL2"), fetch("URL3")];
   const [res1, res2, res3] = await Promise.all(endpoints);
   ```
4. Execution time: **1 second total.** It waits rigidly for the slowest request in the entire array batch to finish before proceeding downward.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** You absolutely mathematically **cannot** use the `await` keyword effectively unless it is completely trapped natively inside a function block rigidly prefixed with the `async` keyword (Top-Level await is limited and bleeding-edge).
- **Gotcha 2:** Junior engineers notoriously forget the second `await` when manipulating JSON `.json()` responses in network fetch operations (`const user = await response.json()`). Because parsing massive megabytes of raw text into structured RAM blocks is CPU intensive, the browser mandates the parse executes asynchronously!
- **Gotcha 3:** `Promise.all` executes with an absolute "Fail-Fast" architecture. If even 1 out of 1,000 batched database requests randomly fails and mathematically rejects, the *entire* chained `Promise.all` algorithm triggers a fatal catch error, destroying the 999 perfectly successful responses entirely. (Use `Promise.allSettled()` if you need all results individually).

### Reflection Question
If you have an `async function parseData() { return 99; }`, why does executing `console.log(parseData())` mathematically log a literal structural `Promise { <fulfilled> }` payload rather than practically logging the physical integer `99`?