# Exercise 007 - Validation & Error Handling

### Objective
Protect your database from "Garbage In." Implement robust schema validation and centralized error handling to ensure your backend remains stable and your data remains clean.

### Core Concepts to Master
- **Schema Validation:** Defining strict rules for incoming data (e.g., "Email must contain an @", "Username must be at least 3 chars").
- **Joi / Zod:** Popular validation libraries that allow you to define data "schemas" in JavaScript.
- **Middlware-based Validation:** Intercepting the request and returning an error before it ever reaches your database logic.
- **Status Code Precision:** Distinguishing between user errors (400 Bad Request) and server errors (500 Internal Server Error).

### Research Topics
- "JavaScript Zod validation library tutorial"
- "Express validation middleware pattern"
- "Standardizing API error responses"

---

### The Practical Challenge

**Part 1: Defining a Validation Schema**
1. Install the `zod` library: `npm install zod`.
2. Define a schema for a new user registration:
   ```javascript
   const { z } = require('zod');
   const userSchema = z.object({
       username: z.string().min(3).max(20),
       email: z.string().email(),
       age: z.number().int().positive().optional()
   });
   ```
3. Test the schema by calling `userSchema.parse({ ... })` with both valid and invalid data objects.

**Part 2: Validation Middleware**
1. Create a reusable middleware function to validate incoming `req.body` data.
2. If validation fails, return a `400 Bad Request` status with the specific error messages from Zod.
3. Apply this middleware to your `POST /users` route:
   `app.post('/users', validate(userSchema), (req, res) => { ... });`

**Part 3: Handling Database Constraint Violations**
1. Your database (SQLite/Postgres) also has rules (e.g., a "Unique" constraint on emails).
2. Attempt to create two users with the same email. Observe the error object thrown by your ORM.
3. Implement a try/catch block around your creation logic to catch these specific database errors and transform them into user-friendly messages rather than exposing raw SQL errors.

**Part 4: Global Error Formatter**
1. Implement a final, global error-handling middleware.
2. Standardize all your errors to return a consistent JSON structure:
   ```json
   {
       "success": false,
       "error": "Validation Failed",
       "details": ["Email is invalid"]
   }
   ```
3. Test the entire flow: Send a malformed request, see the standardized error, then send a valid request and see the success response.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Validating too late. Always perform basic format validation (Zod) *before* hitting the database. This saves server resources and prevents unnecessary database connections for obviously incorrect data.
- **Gotcha 2:** Silencing Errors. Avoid using a "catch-all" `try/catch` that returns the same message for every error. If you are stuck at "Something went wrong," you won't know if the issue was a 404, a 500, or a database timeout.

### Reflection Question
Why is it important to validate data on BOTH the frontend (before the fetch) and the backend (before the database)?