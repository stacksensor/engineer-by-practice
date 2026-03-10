# Exercise 005 - Capstone Build I (Backend & Data)

### Objective
Execute the foundation. Build the backend server, database schema, and API endpoints defined in your Exercise 004 plan, ensuring a solid data layer before building the UI.

### Core Concepts to Master
- **Database Initialization:** Using an ORM (Prisma/Sequelize) to create the physical tables from your Exercise 004 diagram.
- **RESTful Architecture:** Implementing the GET/POST routes to handle CRUD operations for your specific capstone resources.
- **Environment Management:** Using `.env` correctly to store your local database URL and OpenAI secret key.
- **Unit Testing:** Writing basic tests to ensure your API returns the correct JSON data before you connect it to the frontend.

### Research Topics
- "Setting up a Node.js project for a larger app"
- "Testing Express APIs with Supertest"
- "Best practices for folder structure in full-stack projects"

---

### The Practical Challenge

**Part 1: Initializing the Repository**
1. Create a root project folder. Initialize a Git repo.
2. Set up the folder structure:
   - `/backend` (Node/Express)
   - `/frontend` (React/Vite)
3. In the `/backend`, install your dependencies: `express`, `cors`, `dotenv`, and your chosen ORM.

**Part 2: Defining the Master Schema**
1. Code your Models (e.g., User, Recipe, Post) based on your Exercise 004 design.
2. Run your migration tool to create the database tables.
3. Seed the database with 2-3 pieces of "Mock Data" manually so you can test your endpoints immediately.

**Part 3: The API Core**
1. Implement the first two primary endpoints (e.g., `GET /items` and `POST /items`).
2. Verify they work using Postman or `curl`.
3. Ensure the `POST` endpoint correctly validates the incoming body and saves the data to the database permanently.

**Part 4: Connecting the AI**
1. Implement the endpoint that interacts with the OpenAI API.
2. Pass data from the client (e.g., a text prompt) to the model.
3. Take the AI's response and save it to your database as a new record. 
4. Example: A user posts a "Note", AI generates a "Summary", and you save both to the `Notes` table.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** CORS blocks. When your frontend (localhost:5173) talks to your backend (localhost:3000), you will get a CORS error unless you explicitly enable it in your Express app: `app.use(cors())`.
- **Gotcha 2:** Async Handlers. Always wrap your database and AI API calls in `try/catch` blocks. If an external service is down, your entire server will crash unless you handle the error gracefully.

### Reflection Question
Why is it better to build and test the "Backend and Database" before building the "Frontend UI"?