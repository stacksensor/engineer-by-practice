# Exercise 007 - DOM & Browser APIs

### Objective
Stop interacting with your apps strictly through CLI Console.logs. Grasp the native C++ APIs built directly into the Desktop Browser that allow Javascript to physically alter raw HTML structure, inject CSS animations, bind to mouse events, and store persistent hard-drive data.

### Core Concepts to Master
- **The DOM (Document Object Model):** The massive, mutable tree-like programmatic API representation of the physical HTML text elements on your screen.
- **Node Traversing/Querying:** Selecting physical elements out of the DOM securely using logical rules (`getElementById`, `querySelector`).
- **Event Listeners:** Binding callback algorithms natively triggered exclusively by exact user interactions (Clicks, Keypresses, Scrolling).
- **Local Storage:** Securing persistent gigabytes of physical text data within the absolute hardware sandbox limits of the browser, surviving page refreshes natively.

### Research Topics
- "JavaScript querySelector vs getElementById"
- "Adding event listeners JS MDN"
- "Event propagation bubbling vs capturing"
- "Differences between localStorage and sessionStorage"

---

### The Practical Challenge

**Part 1: Injecting HTML via the DOM**
1. Create a raw `index.html` with an empty `div`:
   ```html
   <div id="app-container"></div>
   <script src="app.js"></script>
   ```
2. In `app.js`, query the DOM API to physically grab that empty node structurally out of RAM:
   `const container = document.getElementById("app-container");`
   `const title = document.createElement("h1");`
3. Dynamically inject structural text properties directly into the generated object:
   `title.textContent = "Welcome to the Neural Network.";`
   `title.style.color = "red";`
4. Use `.appendChild()` to forcefully append the floating title element perfectly into the static DOM layout chain:
   `container.appendChild(title);`
5. Refresh the browser. Watch JS render physical graphics entirely outside the scope of raw HTML constraints.

**Part 2: The Event Binding Architecture**
1. Dynamically append a standard button logic element: `<button id="hack-btn">Hack Mainframe</button>`
2. Select it: `const btn = document.querySelector("#hack-btn");`
3. Map an autonomous physical Event Listener straight to the Node:
   ```javascript
   btn.addEventListener("click", (eventObject) => {
       console.log("Triggered physical logic on coordinates:", eventObject.clientX, eventObject.clientY);
       title.style.color = "green";
       title.textContent = "Mainframe Compromised.";
   });
   ```
4. Click the button. Realize the massive paradigm shift: the Javascript logic is no longer running exclusively mathematically top-to-bottom. It physically parked a listener payload into the browser C++ logic loop awaiting a specific physical mouse trigger execution entirely indefinitely.

**Part 3: Local Storage Persistence Engine**
1. Your app immediately dies and reverts to red text if you press F5 Refresh.
2. Inside your button click callback, command the Web Storage API to physically write data to the user's hard drive securely:
   `localStorage.setItem("hackStatus", "success");`
3. Refresh the page entirely.
4. Add startup logic natively tracking the API flag completely structurally out in the global `app.js` scope:
   ```javascript
   const status = localStorage.getItem("hackStatus");
   if (status === "success") {
       title.style.color = "green"; 
       title.textContent = "Welcome Back, Admin.";
   }
   ```
5. Note how it instantly bypasses the start screen logic purely dynamically over multiple browser restarts. Remove it manually using `localStorage.clear();`.

**Part 4: Form Default Overriding**
1. Add an empty form structure: 
   `<form id="login"><input type="text" id="user" /><button type="submit">Go</button></form>`
2. Attach a typical click listener to the Submit interaction:
   `document.querySelector("#login").addEventListener("submit", (e) => { ... });`
3. Attempt to log the exact `user` input value algorithms: 
   `console.log(document.querySelector("#user").value);`
4. Execute it. Notice what violently happens. The physical page instantly flashes and refreshes entirely, instantly deleting your console log history!
5. Add `e.preventDefault();` to the absolute top of the callback. Observe how this overrides and terminates the 25-year-old native 1990s HTML POST logic completely natively.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** A `NodeList` object magically returned by `.querySelectorAll()` mathematically looks identical to an Array `[...]`, but structurally lacks functional array map methods mapping algorithms heavily. Attempting to `.map()` over it crashes. Use `Array.from(nodeList)` or the ES6 `[...nodeList]` spread logic to forcibly cast it into a true structural Array.
- **Gotcha 2:** Injecting massive amounts of raw text algorithms using `.innerHTML = "<script>alert('Hack')</script>"` introduces terrifying XSS (Cross Site Scripting) security liabilities if that text string algorithm includes unsterilized database input variables. `.textContent` strips HTML natively rendering it fundamentally secure.
- **Gotcha 3:** Adding `<script>` tags physically into the `<head>` of HTML entirely blocks visual paints. Always load scripts heavily natively at the absolute bottom boundary inside the </body> limit structure, or declare exactly `<script defer>` mapping algorithms logically.

### Reflection Question
Fundamentally, if millions of people execute native Javascript operations over massive Node servers (Node.JS), why does deploying an `app.js` server framework file mapping `console.log(document.querySelector('body'))` physically instantly throw a fatal Reference Error terminating the entire Node application server processing engine?