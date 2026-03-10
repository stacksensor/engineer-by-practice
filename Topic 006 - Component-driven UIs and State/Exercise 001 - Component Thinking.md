# Exercise 001 - Component Thinking

### Objective
Stop thinking about web pages as massive single documents. Start architecting modular, isolated, reusable UI blocks (Components) that snap together like Lego bricks to build complex applications natively.

### Core Concepts to Master
- **Components:** Independent, reusable pieces of the UI.
- **Declarative vs Imperative UI:** 
  - Imperative (Vanilla JS DOM): "Grab this div, change its color, add this text, append it here."
  - Declarative (React/Vue/Svelte): "Here is the data state. Render the UI to match this data exactly."
- **Props (Properties):** Read-only data passed downwards structurally from a Parent component into a Child component.

### Research Topics
- "Thinking in React by React Docs"
- "React Components vs Elements"
- "Passing Props in React examples"
- "Declarative vs Imperative UI programming"

---

### The Practical Challenge

**Part 1: The Monolith Flaw**
1. Open a CodePen (or use Vite to scaffold a basic vanilla JS app).
2. Build a user profile card imperatively using raw HTML/JS. Create a massive `<div>` containing an image, an `<h2>` name, and a `<p>` bio.
3. Your boss asks you to render 50 unique user profile cards. 
4. Using vanilla JS, you would have to write a massively complex `for` loop executing `document.createElement` dozens of times, manually assigning classes, and painstakingly appending them to the DOM.

**Part 2: Designing the Blueprint**
1. Switch to a component-driven mindset. 
2. Imagine a theoretical `UserProfile` function. If you pass it a JavaScript object `{ name: "Alice", bio: "Developer" }`, it mathematically returns the exact HTML structure perfectly formatted for that specific user.
3. This is a Component. It is a factory that takes raw **Data (Props)** and spits out **UI (HTML)**.

**Part 3: Building a React Component**
1. Scaffold a real React app: Run `npx create-vite@latest my-app --template react` in your terminal, then `cd my-app` and `npm install`.
2. Delete the boilerplate in `src/App.jsx`.
3. Create a new file `src/UserProfile.jsx`.
4. Write a simple JavaScript function:
   ```jsx
   export function UserProfile(props) {
       return (
           <div className="card">
               <h2>{props.name}</h2>
               <p>{props.bio}</p>
           </div>
       );
   }
   ```
5. Notice how we are physically inserting JavaScript variables directly into the HTML structure using `{curly braces}`.

**Part 4: Composing the App**
1. Go back to `App.jsx`. Import your new component: `import { UserProfile } from './UserProfile';`.
2. Render it inside the App component identically to how you would render a native HTML tag, passing data as attributes (Props):
   ```jsx
   export default function App() {
       return (
           <main>
               <UserProfile name="Alice" bio="Senior Developer" />
               <UserProfile name="Bob" bio="UI Designer" />
               <UserProfile name="Charlie" bio="Data Scientist" />
           </main>
       );
   }
   ```
3. Run the app (`npm run dev`). You just rendered 3 distinct UI blocks natively using a single unified architecture.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Props are strictly Read-Only. If you attempt to write `props.name = "Hacked"` inside the `UserProfile` component, React will violently throw a fatal error. Data permanently flows downwards (Parent -> Child). If a Child needs to alter data, the Parent must pass down a function as a prop for the Child to execute.
- **Gotcha 2:** In React Component files (`.jsx`), you must use `className=""` instead of the standard HTML `class=""`. `class` is a reserved JavaScript keyword (used for ES6 Classes), so React mandates `className` to avoid syntax parsing destruction.

### Reflection Question
If you have a complex dashboard with a Sidebar, a Header, and a Main Feed, why does breaking them into `<Sidebar />`, `<Header />`, and `<Feed />` components drastically reduce merge conflicts structurally when 10 different developers are working on the same repository concurrently?