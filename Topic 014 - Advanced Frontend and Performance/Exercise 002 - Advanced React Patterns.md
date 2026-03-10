# Exercise 002 - Advanced React Patterns

### Objective
Build more flexible and reusable UI architectures. Move beyond simple props to master advanced design patterns like Compound Components and Render Props, allowing you to build complex interfaces that are easier to maintain and extend.

### Core Concepts to Master
- **Compound Components:** A pattern where a parent (e.g., `<Tabs>`) and children (e.g., `<Tabs.Item>`) work together implicitly using shared state.
- **Render Props:** A technique for sharing code between React components using a prop whose value is a function that returns a React element.
- **Higher-Order Components (HOCs):** An advanced technique for reusing component logic by wrapping an existing component in a new one.
- **Custom Hooks:** Extracting complex stateful logic into shareable functions (e.g., `useAnalytics` or `useFormState`).

### Research Topics
- "React compound components pattern explained"
- "When to use render props vs custom hooks"
- "Building a flexible Modal with React Patterns"
- "Separation of concerns in React components"

---

### The Practical Challenge

**Part 1: The Compound Menu**
1. Our objective is to build a `Dropdown` component that works like this:
   ```jsx
   <Dropdown>
     <Dropdown.Toggle>Click Me</Dropdown.Toggle>
     <Dropdown.Menu>
       <Dropdown.Item>Edit</Dropdown.Item>
       <Dropdown.Item>Delete</Dropdown.Item>
     </Dropdown.Menu>
   </Dropdown>
   ```
2. Create the `Dropdown` parent. Use `React.useState` to track if the menu is open.
3. Use `React.context` (or `React.Children.map`) to pass the "open" state and the "toggle" function down to the sub-components without requiring the user to pass props manually.
4. Implement the `Toggle`, `Menu`, and `Item` children.

**Part 2: Logic Sharing with Custom Hooks**
1. Build a `useWindowSize` hook that tracks the browser's width and height.
2. In the hook, use `useEffect` to attach a 'resize' listener and clean it up when the component unmounts.
3. Use this hook in two different components: One that changes its layout for mobile, and one that displays the current dimensions on screen.
4. Observe how logic is shared without duplicating code files.

**Part 3: The Render Prop Pattern**
1. Create a `MouseTracker` component that tracks the X/Y coordinates of the cursor.
2. Instead of rendering a specific UI, make it accept a `render` function as a prop:
   `<MouseTracker render={({ x, y }) => ( <h1>Position: {x}, {y}</h1> )} />`
3. Implement a second usage of the same component that renders an image that follows the cursor around.
4. Note how the "Tracking Logic" is completely decoupled from the "Visual UI."

**Part 4: Refactoring to Component Libraries**
1. Review your Compound Dropdown from Part 1.
2. Refactor it to handle keyboard navigation (e.g., using 'Esc' to close).
3. Discuss how these patterns are used in professional libraries like **Headless UI** or **Radix UI**.
4. Wrap one of your components in a simple Higher-Order Component (HOC) called `withLogger` that logs whenever the component is mounted or updated.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Prop Drilling. If you find yourself passing the same prop through 5 layers of components, you should probably be using a Context or a Compound Component pattern instead.
- **Gotcha 2:** Context Overuse. While Context is great for Compound Components, using it for *all* state can make your components harder to test in isolation. Only use Context for truly shared data.

### Reflection Question
Why are "Headless" UI libraries (those that provide logic without styles) becoming the industry standard for enterprise-grade design systems?
