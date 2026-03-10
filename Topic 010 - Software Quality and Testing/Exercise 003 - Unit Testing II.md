# Exercise 003 - Unit Testing II (Mocking)

### Objective
Master test double architecture. Implement sophisticated mocking strategies to completely isolate units of code from unpredictable external dependencies like databases and third-party web services.

### Core Concepts to Master
- **The Concept of Isolation:** A unit test must never access the internet or a live database. If it does, it is an Integration Test.
- **Stubs:** Hardcoded functions that immediately return predefined deterministic payload strings.
- **Mocks:** Programmable tracking functions that record exactly how many times they were invoked and what specific arguments were passed into them.
- **Dependency Injection:** Architecting your functions so that external database connections are passed in dynamically rather than hardcoded internally.

### Research Topics
- "Jest mock functions tutorial"
- "Understanding dependency injection JavaScript"
- "Mocking the Fetch API in Jest"

---

### The Practical Challenge

**Part 1: The Coupled Function**
1. Write a function named `fetchUserList()` that internally executes a standard `fetch('https://api.github.com/users')`.
2. The function parses the JSON and physically returns an array of login names.
3. Write a standard Unit Test for this function.
4. Execute it. You will realize your test takes 400ms to complete, heavily depending entirely on GitHub's active server status. This is architecturally incorrect.

**Part 2: The jest.fn() tracker**
1. Familiarize yourself with Jest tracking natively.
2. Initialize: `const mockCallback = jest.fn()`.
3. Pass `mockCallback` into any looping array method like `.map()`.
4. Assert the exact execution count strictly: `expect(mockCallback.mock.calls.length).toBe(3)`.
5. Check arguments cleanly: `expect(mockCallback.mock.calls[0][0]).toBe('first_argument')`.

**Part 3: Architecting the Mock Environment**
1. To isolate `fetchUserList()`, we must sever the API dependency.
2. Tell Jest to hijack the global window fetch environment.
3. Define the substitution wrapper:
   ```javascript
   global.fetch = jest.fn(() => 
       Promise.resolve({
           json: () => Promise.resolve([{ login: 'FakeUser123' }])
       })
   );
   ```

**Part 4: Executing the Isolated Test**
1. Run your standard unit test logic again.
2. Your local code operates exactly identically, completely unaware that it is speaking to a fake local terminal interceptor rather than GitHub.
3. Your test now resolves in `2ms`.
4. Run `expect(fetch).toHaveBeenCalledTimes(1);` to definitively guarantee your code attempted the network connection.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Junior engineers forget to construct the `mockClear()` teardown hooks between runs. If Test A invokes the mock fetch twice, Test B will mathematically inherit a mock call count of 2 as its starting baseline, abruptly destroying its own `expect(1)` logic sequence.
- **Gotcha 2:** Deeply nested local module requirements (e.g., `import db from './mysqlConnection'`) are notoriously difficult to mock cleanly. Use `jest.mock('./mysqlConnection')` exactly at the absolute top lexical scope of the testing file to overwrite the required module entirely before the test boots.

### Reflection Question
If your heavily mocked unit tests perfectly pass with 100% green accuracy, what structural guarantee do you actually have that the production application will successfully connect to the AWS database layer?