# Exercise 005 - Component Testing (React Testing Library)

### Objective
Master interface verification. Test JavaScript DOM nodes without booting an entire web browser. Use React Testing Library (RTL) to evaluate component accessibility and structural mounting logic.

### Core Concepts to Master
- **JSDOM Framework:** A JavaScript implementation of the HTML standard capable of faking a browser environment inside a Node process.
- **Rendering Virtual Interfaces:** Mounting a UI component strictly in memory to evaluate its internal state hooks.
- **Accessibility Selectors:** Querying elements by standard user-facing attributes (`getByRole`, `getByText`) instead of fragile CSS selectors (`.button-primary`).
- **User Events:** Simulating keyboard typing and mouse interactions synchronously.

### Research Topics
- "React Testing Library vs Enzyme"
- "RTL userEvent vs fireEvent"
- "Testing React hooks with RTL"

---

### The Practical Challenge

**Part 1: The Initial Render**
1. Create a `Button.js` React component. It accepts a `label` string prop and an `onClick` function prop.
2. Initialize `Button.test.js`.
3. Import `render` and `screen` from `@testing-library/react`.
4. Write your first test suite: `test('Button renders its label')`.
5. Call `render(<Button label="Submit Data" />)`.
6. Use `expect(screen.getByText('Submit Data')).toBeInTheDocument()`. JSDOM mounts the virtual component and passes the equality check.

**Part 2: The Action Simulation**
1. We must verify the user interaction works.
2. Initialize a local Jest tracker: `const mockFn = jest.fn()`.
3. Mount the component with the mocked prop: `render(<Button label="Click Me" onClick={mockFn} />)`.
4. Import `userEvent` from `@testing-library/user-event`.
5. Write the simulated click: `await userEvent.click(screen.getByRole('button'))`.
6. Assert the execution: `expect(mockFn).toHaveBeenCalledTimes(1)`.

**Part 3: Testing Active State Changes**
1. Create a complex `Counter.js` component containing a simple numeric state hooked to standard increment buttons.
2. Render `Counter` in the test file.
3. Assert the exact starting numeric value: `screen.getByText('0')`.
4. Trigger `userEvent.click` twice on the increment button.
5. Assert the DOM strictly reads `2`. You validated local React `useState` behavior completely autonomously.

**Part 4: Handling Data Loads**
1. Testing components that fetch API data requires mock promises.
2. Build a `UserList.js` component that displays "Loading..." initially, then uses `useEffect` to trigger an external fetch.
3. Mount the component in the RTL framework.
4. Assert the exact initial loader: `expect(screen.getByText('Loading...')).toBeInTheDocument()`.
5. Await the structural virtual rendering using `screen.findByText(/Username/)`. The `.findBy` prefix returns an implicit promise designed explicitly for React's asynchronous render queues.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Querying nodes by arbitrary `id` attributes breaks tests if the ID changes. Use `getByRole('button')` to guarantee accessibility compliance simultaneously.
- **Gotcha 2:** Ignoring `act({ ... })` warnings. If your component updates state multiple times asynchronously, Jest will throw warnings indicating state updates fell outside the testing wrapper.

### Reflection Question
Why is verifying components identically as a standard human user (by querying visible text) technically superior to validating the underlying React AST directly?