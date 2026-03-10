# Exercise 002 - HTTP Protocol

### Objective
Deconstruct the stateless communication pipeline of the modern web. Master the raw Hypertext Transfer Protocol (HTTP) text formatting that enables servers and clients to exchange structured data payloads reliably.

### Core Concepts to Master
- **Stateless Architecture:** The foundational principle that every HTTP request executes completely independently without any structural memory of the previous interactions.
- **Methods (Verbs):** The explicit intent of the request (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`).
- **Status Codes:** The numerical three-digit integer response dictated by the server indicating success (`200s`), redirects (`300s`), client errors (`400s`), or server catastrophies (`500s`).
- **Headers:** Critical metadata payloads accompanying the primary request (e.g., `Content-Type`, `Authorization`, `Accept`).

### Research Topics
- "HTTP Methods explained"
- "List of common HTTP Status Codes"
- "Understanding HTTP Headers and Body"

---

### The Practical Challenge

**Part 1: The Raw GET Request**
1. Open up Postman, Insomnia, or a raw cURL command line interface.
2. Formulate a primitive `GET` request specifically requesting the public API point: `https://jsonplaceholder.typicode.com/posts/1`
3. Execute the request.
4. Open the raw HTTP output tab. You will physically see the explicit HTTP/1.1 syntax:
   `GET /posts/1 HTTP/1.1`
   `Host: jsonplaceholder.typicode.com`
5. Note the response. A `200 OK` indicates the server successfully parsed the intent and returned a payload.

**Part 2: The Data POST**
1. The `GET` command structurally prevents sending large data bodies. You must use `POST` to generate new server objects.
2. Change your method to `POST`.
3. Set the endpoint to `https://jsonplaceholder.typicode.com/posts`
4. Write a raw JSON body payload correctly:
   ```json
   {
       "title": "foo",
       "body": "bar",
       "userId": 1
   }
   ```
5. You must manually define a Header so the server can mathematically parse your data strings. Set the Header Key: `Content-Type` and Header Value: `application/json`.
6. Send the request. Note the response is structurally now `201 Created`.

**Part 3: Modifying Existing Records**
1. `PUT` operations structurally overwrite the entire target resource natively. `PATCH` operations update partial slices of data.
2. Execute a `PUT` request to `/posts/1`.
3. Send a completely different JSON body.
4. Verify the response confirms the data manipulation success with another HTTP `200` series code.
5. In your network tab, view the raw request mapping again. Notice how the URL contains the explicit target `ID` parameter dynamically (`/1`).

**Part 4: The Fatal Deletion**
1. Select the `DELETE` method.
2. Append the target ID dynamically to the URL endpoint strictly.
3. Fire the request. The server securely responds with either a `200 OK` or structurally a `204 No Content` indicating successful data erasure without a return payload.
4. Attempt to run a standard `GET` request immediately against that deleted ID. 
5. Experience the hallmark `404 Not Found` response code cleanly.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Never execute sensitive data mutations (passwords, banking transfers) via a `GET` request. `GET` parameters are permanently logged directly into local browser history and intermediate ISP router logs securely. Always use `POST` with a hidden HTTPS encrypted body.
- **Gotcha 2:** Ignoring `Content-Type` headers. Sending a beautifully formatted JSON string to a server expecting `application/x-www-form-urlencoded` will cause the server to violently reject it with a `400 Bad Request`. Match the headers exactly to the payload structure.

### Reflection Question
Why will attempting to execute a standard cross-origin AJAX request structurally fail without the explicit presence of specific CORS headers natively transmitted from the external server?