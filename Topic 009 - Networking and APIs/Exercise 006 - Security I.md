# Exercise 006 - Security I (CORS & CSRF)

### Objective
Secure your backend endpoints against unverified external domains and unauthorized cross-site attacks. Master Cross-Origin Resource Sharing (CORS) policies and mitigate Cross-Site Request Forgery (CSRF).

### Core Concepts to Master
- **Same-Origin Policy (SOP):** The fundamental security mechanism restricting how a document or script loaded from one origin can interact with a resource from another origin.
- **Cross-Origin Resource Sharing (CORS):** An HTTP-header-based mechanism that allows a server to indicate any origins (domain, scheme, or port) other than its own from which a browser should permit loading resources.
- **Preflight Requests:** The `OPTIONS` HTTP request the browser automatically sends to check if a CORS operation is permitted before performing the actual `POST` or `PUT`.
- **Cross-Site Request Forgery (CSRF):** A malicious exploit where unauthorized commands are submitted from an authenticated user.

### Research Topics
- "Understanding CORS preflight requests"
- "How do CSRF tokens work"
- "Configuring Express CORS middleware"

---

### The Practical Challenge

**Part 1: Triggering the CORS Block**
1. Initialize a basic Node/Express server running on `http://localhost:3000`. Create a simple `GET /data` endpoint that returns `{"message": "Hello"}`.
2. Open a separate frontend HTML file served on `http://localhost:8080`.
3. Write a raw `fetch("http://localhost:3000/data")` script inside your frontend `index.html`.
4. Run the frontend code and check the browser console. You will see a red error indicating the Fetch was blocked by CORS policy because the `Access-Control-Allow-Origin` header is missing.
5. Note that the server actually received the request, but the browser blocked the response from being accessed by your JavaScript.

**Part 2: Configuring CORS**
1. On your Express server, you must explicitly whitelist the incoming origin.
2. Install the standard security package: `npm install cors`.
3. Configure the middleware to accept only your frontend origin:
   `app.use(cors({ origin: 'http://localhost:8080' }));`
4. Re-run the frontend fetch request. The `GET` command should now succeed.
5. In your network tab, view the raw HTTP response headers and look for `Access-Control-Allow-Origin: http://localhost:8080`.

**Part 3: Exploring CSRF Vulnerabilities**
1. In your frontend application, construct an `<img src="http://localhost:3000/delete-account" />` tag.
2. Notice that browsers execute `GET` requests for images without running standard CORS checks.
3. If this endpoint used session cookies for authentication, the image tag would trigger an account deletion without the user's knowledge.
4. Establish the rule: `GET` endpoints must never perform state-changing operations like deletions or updates.

**Part 4: Implementing CSRF Defenses**
1. CSRF attacks rely on the browser automatically sending cookies with every request.
2. To prevent this, implement a CSRF token system. The server generates a random token and includes it in your frontend forms as a hidden input.
3. When the user submits a form, the token is sent along with the request.
4. The server validates that the submitted token matches the one stored in the user's session.
5. Since an attacker cannot "read" the token from another site, they cannot forge a valid request.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Using `origin: '*'` in production. While this fixes CORS errors during development, it allows any website to make unauthorized requests to your API. Always specify an explicit list of allowed domains.
- **Gotcha 2:** Only protecting against CSRF on state-changing requests. While `GET` requests should be safe, ensure that `POST`, `PUT`, `DELETE`, and `PATCH` are all protected by CSRF tokens if you are using cookie-based authentication.

### Reflection Question
Why do backend-to-backend requests (e.g., using Node's `fetch` or `axios`) bypass CORS restrictions while browser-based requests do not?