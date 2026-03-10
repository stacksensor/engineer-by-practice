# Exercise 004 - TDD Workflow (Red/Green/Refactor)

### Objective
Invert the traditional programming lifecycle. Construct complex logic using Test-Driven Development (TDD) principles to write failing tests before implementing functional code.

### Core Concepts to Master
- **TDD (Test-Driven Development):** The practice of designing software entirely through rigorous testing definitions prior to implementation.
- **Red Phase:** Writing a test expectation that fails because the code does not exist yet.
- **Green Phase:** Writing the minimum feasible code required to make the failing test pass.
- **Refactor Phase:** Optimizing the passing code structurally without breaking the underlying functionality.

### Research Topics
- "TDD red green refactor explained"
- "Test driven development Node JS tutorial"
- "Benefits of Test Driven Development"

---

### The Practical Challenge

**Part 1: The Red Phase Setup**
1. Our objective is to build a string utility function named `camelCaseParser`.
2. Do not write the function yet. Leave the file blank.
3. Open your test spec file and set up a `describe('camelCaseParser')` block.
4. Write your first test case: `test('it handles null inputs by returning an empty string')`.
5. Execute the test: `expect(camelCaseParser(null)).toBe("")`.
6. Verify that your test runner returns a failure indicating the function is undefined.

**Part 2: The Green Phase Execution**
1. Go to your logic file.
2. Implement the bare minimum code to resolve the failure:
   ```javascript
   function camelCaseParser(input) {
       return "";
   }
   ```
3. Re-run your tests. The assertion should now pass.
4. You have achieved your first "Green" phase by writing only the code required to fix the error.

**Part 3: Expanding the Logic Cycle**
1. Write a second test: `test('it returns lowercase strings as-is')`.
2. Assert `expect(camelCaseParser('hello')).toBe('hello')`.
3. The test should fail because your function returns an empty string.
4. Update your logic to handle the new case:
   ```javascript
   function camelCaseParser(input) {
       if (!input) return "";
       return input.toLowerCase();
   }
   ```
5. Your test suite should now be green.

**Part 4: The Refactor Phase**
1. Write a complex test scenario: `expect(camelCaseParser('HELLO_world_app')).toBe('helloWorldApp')`.
2. This will fail your current logic.
3. Implement the full camelCase logic using string manipulation or regular expressions.
4. Once the test passes, use the "Refactor" phase to clean up your implementation (e.g., using more efficient loops or built-in methods) while relying on your tests to ensure no regressions occur.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Skipping the Red Phase. Many developers write the code first and then add a test to confirm it works. This avoids the predictive benefit of TDD, which is to define boundaries before implementation.
- **Gotcha 2:** Writing too much code in the Green Phase. Ensure you only write the necessary logic to make the current failing test pass. This prevents over-engineering and keeps implementations focused.

### Reflection Question
Why does writing tests before implementation often lead to a better separation of concerns and more modular code architecture?