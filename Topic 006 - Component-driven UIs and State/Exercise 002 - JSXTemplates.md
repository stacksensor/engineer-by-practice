# Exercise 002 - JSX & Templating

### Objective
Master JSX (JavaScript XML), the syntax extension that allows developers to write physical HTML-like structural markup deeply natively inside JavaScript logic files.

### Core Concepts to Master
- **JSX:** It looks like HTML, but it is fundamentally pure JavaScript. Babel mathematically transpiles `<h1>Hello</h1>` into `React.createElement('h1', null, 'Hello')`.
- **Dynamic Expressions:** Escaping structural HTML natively using `{ }` to execute raw JavaScript math, ternary logic, or mapped arrays instantly.
- **Fragments `<>`:** A structural boundary requirement that mandates a Component can only physically return one single top-level parent element.

### Research Topics
- "React JSX syntax rules"
- "React Fragments"
- "Rendering lists in React using map"
- "Conditional rendering in React"

---

### The Practical Challenge

**Part 1: The Fragmentation Rule**
1. Open your React terminal app from Exercise 1. Create `Sandbox.jsx`.
2. Write a component function trying to return two adjacent `<p>` tags:
   ```jsx
   export function Sandbox() {
       return (
           <p>Paragraph 1</p>
           <p>Paragraph 2</p>
       );
   }
   ```
3. Look at your editor. It instantly throws a fatal syntax error! JSX mandates a single wrapper element.
4. Wrap them in a JSX Fragment (`<>...</>`) to group them structurally without injecting useless `<div>` tags into your actual DOM:
   ```jsx
       return (
           <>
               <p>Paragraph 1</p>
               <p>Paragraph 2</p>
           </>
       );
   ```

**Part 2: Dynamic Expressions and Logic**
1. JSX allows you to pause HTML logic and inject raw JS natively. 
2. Define a variable: `const randomNum = Math.random();`
3. Render it directly into the markup: `<h2>Your lucky number is {randomNum}</h2>`.
4. Run conditional logic internally using a Ternary operator:
   ```jsx
   <p>
       {randomNum > 0.5 ? "You win!" : "You lose."}
   </p>
   ```
5. Note: You cannot use standard `if/else` statements directly inside JSX markup. You must use Ternaries `? :` or short-circuit Operators `&&`.

**Part 3: Rendering Massive Arrays**
1. Create a dummy array of data physically outside the function:
   `const tasks = ["Buy Milk", "Clean Code", "Deploy Server"];`
2. You need to dynamically map these strings into physical `<li>` tags.
3. Inside your `<ul>` tag, escape into JS using `{ }`, and use the Functional `.map()` engine:
   ```jsx
   <ul>
       {tasks.map(task => (
           <li>{task}</li>
       ))}
   </ul>
   ```
4. Run the app. Notice your console throws an angry red warning: "Each child in a list should have a unique 'key' prop."

**Part 4: The React 'Key' ID**
1. The DOM API is notoriously slow. React optimizes this by keeping an invisible mathematical representation of the DOM in RAM (The Virtual DOM). 
2. When a list changes natively, React mathematically compares the Virtual list to the real list. If the `<li>` tags lack unique identifiers, React must completely delete and rebuild the entire list computationally.
3. Add a strict string identifier to fix the loop perfectly:
   ```jsx
   <ul>
       {tasks.map((task, index) => (
           <li key={index}>{task}</li>
       ))}
   </ul>
   ```
4. *Disclaimer:* Using the array `index` as a key is fundamentally dangerous if the array can be sorted or filtered dynamically. Always use a rigid database ID (e.g. `key={task.id}`) in production!

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Remembering that JSX strictly mandates all tags must be closed. In normal HTML, `<input>` and `<br>` are "void elements" and mathematically valid. In JSX, they will violently crash the build. You must forcefully self-close them: `<input />` and `<br />`.
- **Gotcha 2:** HTML structurally commands inline styles using a physical string: `style="color: red; padding: 10px;"`. JSX completely abandons this string for a structural JavaScript Object dictionary: `style={{ color: "red", padding: "10px" }}`. Note the double curly braces (one to escape JSX, one defining the object natively) and the camelCase property mapping.

### Reflection Question
If Babel mathematically compiles your JSX syntax `<button onClick={shoot}>Fire</button>` entirely into raw JavaScript native `React.createElement()` commands behind the scenes, why does building a UI explicitly in JSX dramatically accelerate human engineering speed?