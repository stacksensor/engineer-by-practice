# Exercise 006 - Capstone Build II (Frontend & Integration)

### Objective
Assemble the Interface. Construct the React frontend to consume your custom API, manage application state, and display AI-generated results in a clean, professional user interface.

### Core Concepts to Master
- **State Lifting vs Local State:** Deciding where your data lives (e.g., in a global Context for user auth, or local state for a form).
- **Effect Hooks (`useEffect`):** Fetching data from your backend exactly once when the component mounts.
- **Conditional Rendering:** Showing loading spinners while the AI is thinking, or displaying error messages if the fetch fails.
- **Form Management:** Capturing user input and sending it to the backend as a JSON payload.

### Research Topics
- "Fetching data in React with Axios or Fetch"
- "Implementing a loading spinner in React"
- "React state management patterns for 2024"

---

### The Practical Challenge

**Part 1: The UI Component Shell**
1. In your `/frontend` folder, initialize a Vite React project.
2. Build the structural layout: A Header, a Sidebar (if needed), and a Main Content area.
3. Stub out your main pages (Dashboard, Create, Settings) using simple JSX.

**Part 2: The Data Fetch**
1. Create a "List" view (e.g., `RecipesList`).
2. Use `useEffect` to call your backend `GET /api/recipes` endpoint.
3. Map over the resulting array and display individual cards for each item in the database.
4. Verify that data added via Postman now appears automatically in your React UI.

**Part 3: The Interaction Loop**
1. Build the "Create" form. Capture user inputs (strings, files, or toggles).
2. Wire up the `POST` request. 
3. After a successful save, automatically redirect the user back to the Dashboard or update the list state.

**Part 4: The AI Feedback Loop**
1. This is the "Magic" moment of your Capstone.
2. Implement a dedicated button/form that triggers your backend AI endpoint.
3. Show a localized "Processing..." or "Thinking..." state on the button itself.
4. Once the AI response arrives, update the UI with the fresh content (e.g., a summarized text box or an analyzed image result).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Infinite Loops. If you perform a `fetch` inside a `useEffect` but forget the empty dependency array `[]`, your component will fetch, update state, re-render, fetch again, and eventually crash your browser.
- **Gotcha 2:** Undefined Data. When the app first loads, your state is likely `null` or `[]`. Trying to access `data.user.name` before the fetch finishes will crash the app. Use optional chaining (`data?.user?.name`) or loading guards.

### Reflection Question
How does the use of "Loading States" significantly improve the User Experience (UX) of an application that relies on external AI models that may take 5-10 seconds to respond?