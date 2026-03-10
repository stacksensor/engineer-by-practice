# Exercise 003 - REST API Design

### Objective
Graduate from consuming endpoints to architecting structurally sound, semantic APIs. Understand the constraints of Representational State Transfer (REST) to build predictable and scalable server maps.

### Core Concepts to Master
- **Resource Naming:** Using clean, noun-based URL structures (e.g., `/users` instead of `/getUsers`).
- **Idempotency:** Ensuring that repeating a request (like `PUT` or `DELETE`) multiple times results in the same server state as the first request.
- **RESTful Endpoints:** Standardizing the paths that map to standard CRUD (Create, Read, Update, Delete) operations.
- **Statelessness:** Ensuring the server does not store client session data, requiring each request to contain all necessary information for processing.

### Research Topics
- "REST API naming best practices"
- "HTTP Idempotence explained"
- "CRUD to REST endpoint mapping"

---

### The Practical Challenge

**Part 1: Defining the Resource Map**
1. Plan a blog API for "Articles." 
2. Map the five core RESTful operations to their respective HTTP methods and endpoints:
   - List all articles
   - Retrieve a single article
   - Create a new article
   - Update an existing article
   - Delete an article
3. Ensure you are using nouns and the correct HTTP verbs (GET, POST, PUT/PATCH, DELETE).

**Part 2: Nested Resources**
1. Design endpoints for resources that belong to other resources (e.g., Comments belonging to Articles).
2. Use hierarchical paths like `/articles/:id/comments`.
3. Plan the endpoint to create a new comment for a specific article.
4. Observe how the URL structure clarifies the relationship between the data points.

**Part 3: Versioning and Pagination**
1. Practice API versioning by prepending a version string to your routes (e.g., `/api/v1/articles`).
2. Implement pagination logic for a "List" request to handle large datasets.
3. Use query parameters for filtering and shaping the data: `/api/v1/articles?limit=10&offset=20`.
4. Note how this allows the client to control the volume of data received without changing the resource path.

**Part 4: Handling Errors Semantically**
1. Define the correct HTTP status codes for common failure scenarios (404 for missing items, 401 for missing auth, etc.).
2. Design a standardized error response body so the client knows how to parse failures:
   ```json
   {
       "error": "Not Found",
       "message": "The article with ID 50 was not found.",
       "documentation_url": "https://api.example.com/docs/errors/404"
   }
   ```
3. Implement these checks in a mock server logic.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Using singular nouns or verbs in URLs. REST paths should represent "collections" (e.g., `/users/123`), not actions (e.g., `/getUser/123`).
- **Gotcha 2:** Returning `200 OK` for error responses. Even if your JSON body says "error," the HTTP status code should accurately reflect the failure (e.g., 400, 403, or 500) so that generic HTTP clients can handle the response correctly.

### Reflection Question
Why are `POST` requests typically considered non-idempotent, while `PUT` requests are mandated to be idempotent in the REST specification?