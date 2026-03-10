# Exercise 002 - Unit Testing I (Jest Basics)

### Objective
Graduate from custom testing runners to a professional test framework. Master the Jest ecosystem to orchestrate test suites, isolate dependencies, and evaluate algorithmic accuracy.

### Core Concepts to Master
- **Jest Framework:** The standard JavaScript testing tool providing the `describe`, `test`, and `expect` syntax.
- **Assertions (Expectations):** Declarative validation statements used to verify precise code outputs (e.g., `expect(x).toBe(5)`).
- **Test Suites (Describe Blocks):** Logical groupings that isolate separate functional responsibilities into structured modules.
- **Setup & Teardown:** Lifecycle hooks like `beforeEach` used to prepare or clean up the environment before each test.

### Research Topics
- "JavaScript Jest matchers tutorial"
- "Jest describe, test, and expect syntax"
- "How to run Jest tests from the command line"

---

### The Practical Challenge

**Part 1: The Jest Installation**
1. Initialize a new Node.js project: `npm init -y`.
2. Install Jest as a development dependency: `npm install --save-dev jest`.
3. Add a test script to your `package.json`:
   ```json
   "scripts": {
       "test": "jest"
   }
   ```
4. Create a folder named `src` and a file named `math.js`. Export a simple `add(a, b)` function.
5. Create a `tests` folder and a file named `math.test.js`. Import the `add` function.

**Part 2: The Assertion Pipeline**
1. Implement your first test using the standard Jest syntax:
   ```javascript
   describe('Math Operations', () => {
       test('adds 1 + 2 to equal 3', () => {
           expect(add(1, 2)).toBe(3);
       });
   });
   ```
2. Run `npm test` in your terminal. Ensure the test passes.
3. Observe how the `describe` block organizes the output in the terminal.

**Part 3: Matcher Fundamentals**
1. Explore different Jest matchers. Add tests to verify:
   - Object equality using `.toEqual()` (explain why `.toBe()` fails on objects).
   - String patterns using `.toMatch()` (use a regex to check an email format).
   - Truthiness using `.toBeTruthy()` and `.toBeFalsy()`.
   - Array contents using `.toContain()`.
2. Implement an error-throwing case and use `expect(() => functionCall()).toThrow()` to catch it.

**Part 4: Test Lifecycle**
1. Create a simple `UserStore` class that manages an internal array of users.
2. Write a test that adds a user to the store.
3. Write a second test that checks if the store is originally empty.
4. Observe how the second test fails because the first test modified the global store state.
5. Implement a `beforeEach(() => { ... })` hook in your test file to reset the `UserStore` before every test case to ensure isolation.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Asynchronous Tests. If you are testing a function that returns a Promise, you must either `return` the expectation or use `async/await` within the test block. Otherwise, the test will finish before the code executes, leading to "false positive" passes.
- **Gotcha 2:** Deep Equality. Remember that `.toBe()` checks for referential identity (the same memory address). For arrays and objects, always use `.toEqual()` to recursively check every property.

### Reflection Question
Why does Jest execute tests in a simulated `jsdom` environment rather than launching an actual web browser like Chrome?