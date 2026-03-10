# Exercise 003 - Middleware

### Objective
Master the "Request-Response pipeline." Implement Express middleware to intercept, log, and authorize incoming network traffic before it ever reaches your business logic.

### Core Concepts to Master
- **Middleware Functions:** Functions that have access to the `req`, `res`, and the `next` function in the application’s request-response cycle.
- **The next() Function:** A mandatory callback that signals Express to move to the next middleware in the stack. Forgetting this will "hang" the request indefinitely.
- **Global vs Route-Specific Middleware:** Applying logic to every single request (like logging) versus specific protected endpoints (like authentication).
- **Built-in Middleware:** Using standard Express functions like `express.json()` to automatically parse incoming data bodies.

### Research Topics
- "Writing custom middleware Express"
- "Express router-level middleware vs app-level middleware"
- "Commonly used Express middleware (morgan, helmet)"

---

### The Practical Challenge

**Part 1: The Custom Logger**
1. In your `server.js` file, create a function that logs every incoming request.
2. The function should print the timestamp, the HTTP method (GET, POST), and the URL.
3. Apply it globally using `app.use()`:
   ```javascript
   app.use((req, res, next) => {
       console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
       next();
   });
   ```
4. Verify that every time you refresh your browser, a new log appears in your terminal.

**Part 2: The Body Parser**
1. By default, Express cannot read the body of a `POST` request (it arrives as a stream of raw bytes).
2. Use the built-in middleware to enable JSON parsing:
   `app.use(express.json());`
3. Create a `POST /echo` route that returns `res.json(req.body)`.
4. Use a tool like Postman, Insomnia, or simple `fetch` to send a JSON object. Ensure the server echoes it back accurately.

**Part 3: Route-level Authentication**
1. Create a middleware function named `checkAuth`.
2. This function checks if a specific query parameter `?apiKey=12345` is present in the URL.
3. If it exists, call `next()`. If not, send a `401 Unauthorized` response.
4. Apply this middleware sparingly to ONLY one specific route:
   `app.get('/admin', checkAuth, (req, res) => { res.send('Welcome, Admin'); });`
5. Verify that `/admin` is blocked without the key, while your `/` route remains accessible.

**Part 4: Handling Errors**
1. Express has a special signature for error-handling middleware: it takes four arguments `(err, req, res, next)`.
2. Define this at the very bottom of your file.
3. Create a route that intentionally throws an error:
   ```javascript
   app.get('/broken', (req, res) => {
       throw new Error('Something went wrong!');
   });
   ```
4. Use your error middleware to catch this and return a clean JSON error message to the client instead of a HTML stack trace.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Calling `res.send()` and `next()` in the same function. Once a response is sent to the client, you cannot "move on" to the next middleware or send headers again. This will cause an "Headers already sent" error.
- **Gotcha 2:** Order of Operations. Middleware is executed in the order it is defined. If you place your `express.json()` parser *below* your routes, your routes will see `req.body` as `undefined`.

### Reflection Question
Why is the "pipeline" architectural pattern of middleware more efficient than writing authentication and logging code separately inside every individual endpoint function?