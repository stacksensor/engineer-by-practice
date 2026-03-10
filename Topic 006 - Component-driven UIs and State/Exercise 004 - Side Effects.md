# Exercise 004 - Side Effects (useEffect)

### Objective
Synchronize your sterile mathematical Component logic with external non-React systems perfectly (like fetching Database APIs, starting Browser Timers, or directly manipulating Document metadata) without trapping your UI entirely in infinite recursive render logic loops.

### Core Concepts to Master
- **Pure Functions:** React requires Components to strictly act purely. Given Data X, it must absolutely predictably return UI Y natively, without altering any physical external servers or databases simultaneously during calculation.
- **Side Effects:** Any logic that mathematically escapes the boundary of the React component (fetching data, altering localStorage, mapping an event listener to the global `window`).
- **The `useEffect` Dependency Array:** The exact mathematical tracking system telling React exactly *when* an effect payload should fire rigidly (On mount, on specific data change, or flawlessly on every render).

### Research Topics
- "React useEffect hook syntax"
- "React pure functions and side effects"
- "Understanding useEffect dependency array"
- "Cleanup functions in useEffect"

---

### The Practical Challenge

**Part 1: The Infinite Loop Trap**
1. Start an empty Component returning a `<div>`. Initialize State: `const [data, setData] = useState([]);`
2. Write a native `fetch` command directly structurally inside the function body exactly before the return block:
   ```jsx
   fetch("https://jsonplaceholder.typicode.com/todos")
      .then(res => res.json())
      .then(json => setData(json));
   ```
3. Look at your browser network tab. It is frantically executing hundreds of identical network API requests every single second!
4. *Reason:* The Component mathematically mapped the function natively. It hit `fetch`. `fetch` eventually triggered `setData`. `setData` explicitly forces React to re-render the Component computationally perfectly from the absolute top. React hits the `fetch` again. Loop violently forever until memory exhausts entirely.

**Part 2: Controlling the Effect**
1. Import strongly: `import { useEffect } from 'react';`
2. Wrap your entire `fetch` block perfectly natively inside the Hook wrapper logic.
   ```jsx
   useEffect(() => {
       fetch("https://jsonplaceholder.typicode.com/todos")
          .then(res => res.json())
          .then(json => setData(json));
   }); 
   ```
3. It's still infinitely looping! You completely forgot the paramount mechanism: **The Dependency Array**.
4. Pass an entirely empty array `[]` explicitly as the exact mathematical second parameter directly to the hook strictly:
   `useEffect(() => { ...fetch logic... }, []);`
5. Check your network tab. You fired exactly one, flawless, highly structured network API request purely when the component mathematically Mounted (appeared physically on screen).

**Part 3: Tracking Data Dependencies**
1. Build a Button UI manipulating a localized `userId` integer state completely:
   `const [userId, setUserId] = useState(1);`
2. You need your `useEffect` algorithm strictly to grab new payload JSON entirely conditionally precisely every time the user wildly clicks the button to change the `userId` specifically.
3. Update the fetch URL natively dynamically: 
   `fetch("https://jsonplaceholder.typicode.com/users/" + userId)`
4. The empty `[]` bracket array mathematically blocks the hook from firing entirely unconditionally again.
5. Explicitly inject the `userId` state heavily into the physical tracker array: `[userId]`.
6. Click the button. React perfectly observes the exact mutation of the `userId` integer in RAM, intentionally executes your `useEffect` payload securely passing the new ID, and repaints perfectly.

**Part 4: Memory Leak Cleanup**
1. Assume you explicitly attach a scrolling Event Listener mapping autonomously directly to the global Window natively inside an effect hook when a `Modal` component pops up perfectly:
   ```jsx
   useEffect(() => {
       window.addEventListener("scroll", trackScroll);
   }, []);
   ```
2. When the user closes the Modal, React completely logically destroys the Component securely mathematically.
3. However, the Browser Window rigidly mathematically retains your physical "scroll" algorithm natively parked heavily in memory forever! Open the Modal 50 times, you spawn 50 permanent background loops. A massive Memory Leak.
4. Provide a `Cleanup Function` rigorously natively. The `useEffect` arrow function can explicitly return a secondary function algorithm React will mathematically universally execute exactly seconds before structurally obliterating the Component:
   ```jsx
   useEffect(() => {
       window.addEventListener("scroll", trackScroll);
       return () => { window.removeEventListener("scroll", trackScroll); };
   }, []);
   ```
5. The component is entirely natively, perfectly self-contained safely.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** A `useEffect` Hook securely strictly physically executes **after** React finishes rendering and physically paints the DOM markup heavily to the browser screen completely natively. It does not block painting (unlike legacy lifecycle methods).
- **Gotcha 2:** It is mathematically absolutely impossible to natively pass an ES8 `async` payload directly unconditionally effectively to a `useEffect` syntax boundary (e.g. `useEffect(async () => {})`). `useEffect` demands the payload return specifically a Cleanup function entirely synchronously or absolutely nothing. You must define your `async` fetching function dynamically *inside* the effect, and forcefully execute it identically: `useEffect(() => { const go = async () => {}; go(); }, [])`.
- **Gotcha 3:** Heavily logging a Javascript State variable conditionally inside `useEffect` natively instantly after triggering a rigid `setCount()` logic algorithm will frustratingly print absolute stale mathematical data definitively. State updates structurally process queue sequences fully asynchronously exactly entirely.

### Reflection Question
Why will attempting to conditionally structurally wrap a React Hook inside an `if` block (`if (x > 5) { useEffect(...) }`) mathematically immediately violently crash your entire application natively?