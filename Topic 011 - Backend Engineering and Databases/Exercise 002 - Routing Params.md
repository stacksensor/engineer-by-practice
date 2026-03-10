# Exercise 002 - Routing & Params

### Objective
Expand your server's navigation capabilities. Implement dynamic route segments to handle thousands of unique resource requests (like user profiles or product pages) with a single logical endpoint pattern.

### Core Concepts to Master
- **URL Parameters (Path Params):** Variable segments in a URL (e.g., `/users/:id`) used to identify specific resources.
- **Query Parameters:** Key-value pairs appended to a URL (e.g., `/search?q=term`) used for filtering, sorting, or searching.
- **Named Captures:** Express's ability to extract these variables and place them into the `req.params` and `req.query` objects automatically.
- **Route Specificity:** Understanding how Express matches routes from top-to-bottom and how to avoid overlapping patterns.

### Research Topics
- "Express.js route parameters vs query strings"
- "How to access req.params in Express"
- "URL encoding and decoding in JavaScript"

---

### The Practical Challenge

**Part 1: The Dynamic Profile**
1. In your `server.js` file, create a route pattern for user profiles.
2. Use the colon syntax to define a variable segment:
   ```javascript
   app.get('/users/:username', (req, res) => {
       const user = req.params.username;
       res.send(`User Profile for: ${user}`);
   });
   ```
3. Boot the server and visit `http://localhost:3000/users/alice` and `http://localhost:3000/users/bob`.
4. Observe how a single block of code handles multiple unique identities.

**Part 2: The Search Engine**
1. Implement a search endpoint utilizing query parameters.
2. Unlike path params, query strings are not defined in the route path directly.
3. Access the values using `req.query`:
   ```javascript
   app.get('/search', (req, res) => {
       const { category, price } = req.query;
       res.send(`Searching for ${category} under $${price}`);
   });
   ```
4. Test by visiting `http://localhost:3000/search?category=laptops&price=500`.

**Part 3: Handling Multiple ID Segments**
1. Combine multiple parameters to identify nested resources.
2. Create a route for a specific photo within an album:
   `app.get('/albums/:albumId/photos/:photoId', (req, res) => { ... });`
3. Extract both `albumId` and `photoId` from `req.params`.
4. Return a JSON object confirming the retrieved IDs to verify the extraction logic.

**Part 4: Route Ordering and Catch-alls**
1. Create a "Fallback" or "404" route.
2. Use the wildcard symbol `*` at the very end of your file:
   ```javascript
   app.get('*', (req, res) => {
       res.status(404).send('Resource Not Found');
   });
   ```
3. Move this route to the top of the file (before `/users/:username`).
4. Re-run your server. You will notice that *every* request now returns the 404 message.
5. Move the wildcard route back to the bottom. This demonstrates the critical importance of route ordering in Express.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Overlapping Routes. If you have `/users/new` and `/users/:id` defined, and `/users/:id` comes first, the string "new" will be treated as an ID, and the "new" route will never be reached. Always place specific routes above generic variable routes.
- **Gotcha 2:** Undefined Params. If you try to access `req.params.userID` but your route is defined as `/users/:id`, the value will be `undefined`. Ensure the key in `req.params` exactly matches the name used in the route string.

### Reflection Question
When should you use a Path Parameter (e.g., `/items/5`) versus a Query Parameter (e.g., `/items?id=5`) when designing a RESTful API?