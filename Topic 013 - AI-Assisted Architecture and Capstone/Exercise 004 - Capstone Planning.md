# Exercise 004 - Capstone Planning (Architecture & Specs)

### Objective
Transition from "Exercises" to a "Product." Define the scope, technology stack, and user stories for your final Capstone Project, demonstrating your ability to plan a full-stack, AI-enhanced application from scratch.

### Core Concepts to Master
- **Problem Statement:** Identifying a real-world problem that your application will solve.
- **MVP (Minimum Viable Product):** Stripping your idea down to the absolute core features required to prove it works.
- **Tech Stack Selection:** Justifying your choice of Frontend (React/Vite), Backend (Node/Express), Database (SQL/Prisma), and AI integration (OpenAI).
- **User Stories:** Defining features from the user's perspective (e.g., "As a user, I want to upload a photo and get an AI summary").

### Research Topics
- "How to plane an MVP for a coding project"
- "Software Architecture Diagram basics"
- "Defining user stories for web apps"

---

### The Practical Challenge

**Part 1: The Elevator Pitch**
1. Define your project in one sentence. It must involve:
   - A Frontend (React)
   - A Backend API (Express)
   - A Database (SQL)
   - An AI Feature (Summarization, Image analysis, or Chat)
2. Example: "A smart Recipe Manager where users upload photos of ingredients, and AI suggests a 15-minute healthy meal which is then saved to a personal database."

**Part 2: The Data Schema**
1. Draw the Entity Relationship Diagram (ERD) for your database.
2. What tables do you need? (e.g., `Users`, `Recipes`, `Ingredients`).
3. Define the primary and foreign keys. This plan will serve as your blueprint for Exercise 005.

**Part 3: The API Map**
1. List every RESTful endpoint your application will require.
2. Example: 
   - `POST /upload-photo`
   - `GET /recipes`
   - `POST /save-recipe`
3. Decide where the AI call happens. Does the frontend call OpenAI directly, or does the backend handle it? (Hint: Backend is more secure for API keys).

**Part 4: The UI/UX Wireframe**
1. Sketch (or use a tool like Figma/Excalidraw) the three main screens of your app:
   - Dashboard/Home
   - Action Screen (e.g., The AI Upload)
   - Profile/Collection Screen
2. Identify the core user "Happy Path"—the sequence of clicks a user takes to achieve the main goal.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Scope Creep. Junior developers often try to build "Facebook for Dogs with AI and Crypto." Your Capstone must be achievable in 1-2 weeks. Focus on one core feature done perfectly rather than ten features done poorly.
- **Gotcha 2:** Ignoring Data Persistence. Ensure your AI feature actually "does something"—saving the result to a database is vital for a true full-stack project.

### Reflection Question
Why is the planning phase (Wireframing, Schema design) considered 50% of the total work for a Senior Developer, even if they haven't written a single line of code yet?