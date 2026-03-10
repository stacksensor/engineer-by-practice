# Exercise 006 - End-to-End Testing (Cypress)

### Objective
Abandon simulated DOM testing for physical browser automation. Configure Cypress to boot a full Chromium engine, navigate local web servers, and inject real keyboard strokes into active interfaces.

### Core Concepts to Master
- **Cypress Architecture:** A Node runtime spinning an actual physical web browser directly connected to the local development server.
- **Selector Engine:** Targeting physical DOM nodes loaded correctly within the full webpage context.
- **Command Assertions:** Ensuring page redirects and API calls finish accurately before clicking subsequent buttons.
- **E2E Flakiness:** The instability of tests completely reliant on network latency and browser rendering queues.

### Research Topics
- "Cypress testing crash course"
- "End to End test vs Integration test"
- "Intercepting network calls Cypress"

---

### The Practical Challenge

**Part 1: The First Launch**
1. Initialize a basic local HTML/CSS/JS frontend server on port 3000.
2. Install Cypress via `npm install cypress --save-dev`.
3. Open the GUI runner via `npx cypress open`.
4. Configure standard E2E testing locally.
5. Create a `login.cy.js` spec file.
6. Write the foundational block: `describe('Authentication Flow')`.

**Part 2: Navigating the DOM**
1. Tell Cypress exactly where to go.
2. Define `beforeEach(() => { cy.visit('http://localhost:3000/login'); })`.
3. Create the first test: `it('Render the login button successfully')`.
4. Assert the core DOM logic: `cy.get('button[type="submit"]').should('exist')`.
5. Save the file. The Cypress GUI automatically re-runs the browser entirely.

**Part 3: The Automated Bot**
1. Script the login process.
2. Chain the commands physically.
3. Fetch the input: `cy.get('input[name="username"]').type('admin')`.
4. Fetch the password box: `cy.get('input[name="password"]').type('secret123')`.
5. Fire the DOM event: `cy.get('button[type="submit"]').click()`.
6. Assert the browser redirects. Verify the URL matches `/dashboard`.
7. Assert exactly the text `Welcome Admin` natively mounts on the screen.

**Part 4: Intercepting Backends**
1. E2E tests physically hit real API servers, burning money and destroying clean databases.
2. Learn `cy.intercept()`.
3. Hijack the `POST /api/login` network request securely.
4. Replace the live AWS server ping entirely with a fake local JSON payload: `{ success: true, token: "mock_abc" }`.
5. Cypress effectively fakes the backend response while maintaining 100% accurate physical browser DOM interactions.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Attempting to force an E2E test to sleep with arbitrary `cy.wait(5000)` pauses. Network calls fluctuate unpredictably. Use Cypress element retries to wait for specific DOM mutations organically.
- **Gotcha 2:** Junior QA teams write a single enormous Cypress test clicking 50 consecutive links. If step 3 fails, the remaining 47 steps are aborted. Always write small test scripts.

### Reflection Question
If E2E testing evaluates the complete software stack physically, why does the Testing Pyramid dictate minimizing active E2E scripts dynamically?