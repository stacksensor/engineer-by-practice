# Exercise 001 - Error Monitoring (Sentry/LogRocket)

### Objective
Stop flying blind. Implement a real-time error tracking system (like Sentry) in your application to automatically capture, aggregate, and alert you to every crash, failed network request, or JavaScript error that users experience in the wild.

### Core Concepts to Master
- **Error Aggregation:** Grouping thousands of identical errors into a single "Issue" so you aren't overwhelmed by alerts.
- **Source Maps:** Uploading your minified production code mapping files so Sentry can show you the exact line of original code where the error occurred.
- **Contextual Data:** Automatically capturing the user's browser version, operating system, and the "Breadcrumbs" (actions they took) leading up to the crash.
- **Alerting Rules:** Configuring thresholds (e.g., "Email me only if this error happens to 50+ unique users").

### Research Topics
- "What is Sentry and why use it for error tracking?"
- "Uploading source maps to Sentry with Vite"
- "Sentry vs LogRocket vs New Relic"
- "Best practices for error logging in production"

---

### The Practical Challenge

**Part 1: The Sentry Integration**
1. Create a free account at [Sentry.io](https://sentry.io).
2. Create a "Project" for a React or Node.js application.
3. Install the SDK: `npm install @sentry/react`.
4. Initialize the SDK in your `index.js`.
5. Intentionally add a "Crash Button" that calls a function that does not exist.
6. Click the button and watch the error appear in the Sentry dashboard in seconds.

**Part 2: The Mystery of Minified Code**
1. Build your app for production: `npm run build`.
2. Observe the resulting `.js` files. They are unreadable, minified messes.
3. Run the production build and trigger your "Crash Button."
4. Observe the Sentry report. It shows an error at `main.asdf234.js:1:567`. This is useless.
5. Manually upload your `.map` files to Sentry. 
6. Refresh Sentry. It should now magically show you the exact original file and line number.

**Part 3: Breadcrumbs & Sessions**
1. Sentry doesn't just show the error; it shows the "History."
2. Create a sequence of actions: Click Button A -> Toggle Switch B -> Click Crash Button.
3. View the "Breadcrumbs" in the Sentry report. 
4. This allows you to recreate the user's exact path to the bug without asking them for a screen recording.

**Part 4: Custom Context**
1. Sometimes you need to know *who* the user was.
2. Use `Sentry.setUser({ id: '123', email: 'test@example.com' });` in your login logic.
3. Trigger the error again.
4. Verify that you can now see the specific user ID associated with the crash. This is vital for customer support and high-priority bug fixing.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Exposing Secrets. Never log actual passwords, credit card numbers, or API keys to Sentry. Sentry offers "Data Scrubbing" features; ensure they are enabled for sensitive fields.
- **Gotcha 2:** Spiking Volume. If you have a bug in a loop that triggers 1 million times, Sentry will reach your monthly plan limit in minutes. Always use "Sampling" (e.g., only capture 10% of errors) in high-traffic production environments.

### Reflection Question
Why is an automated error tracker better than relying on users to email you "Hey, the site crashed"?
