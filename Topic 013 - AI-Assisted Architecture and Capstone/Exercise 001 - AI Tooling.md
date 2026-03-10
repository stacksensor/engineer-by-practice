# Exercise 001 - AI Tooling (Copilot/Cursor)

### Objective
Enhance your biological coding speed. Integrate AI-assisted engineering tools (like GitHub Copilot, Cursor, or ChatGPT) into your daily workflow to automate boilerplate generation, documentation, and logic refactoring.

### Core Concepts to Master
- **Autocomplete & Ghost Text:** The "Next-Token Prediction" model where the IDE predicts the next five lines of code based on your current context.
- **Chat-Driven Development:** Using conversational AI to explain complex external libraries or debug cryptic terminal errors.
- **Context Awareness:** Understanding how AI tools read your open files, directory structure, and comments to provide relevant suggestions.
- **Verification over Trust:** The critical skill of auditing AI-generated code for security flaws, hallucinations, or outdated syntax.

### Research Topics
- "How GitHub Copilot uses local context"
- "Cursor vs VS Code for AI-assisted coding"
- "Risks of AI-generated security vulnerabilities"

---

### The Practical Challenge

**Part 1: Setting up the Assistant**
1. Install an AI coding extension (GitHub Copilot, Codeium, or the Cursor IDE).
2. Create a new file named `server.js`.
3. Write a comment describing a complex function: `// Function to generate a random hex color code and return its HSL equivalent`.
4. Wait for the "Ghost Text" to appear. Press `Tab` to accept it. 
5. Notice how the AI inferred the logic from your comment alone.

**Part 2: The Conversational Debugger**
1. Intentionally break a complicated piece of code (e.g., a regex or a nested loop).
2. Copy the code and the resulting error message from your terminal.
3. Paste both into the AI Chat interface. Ask: "Why is this code throwing X error, and what is the most efficient way to fix it?"
4. Review the explanation. Do not just copy-paste the fix; ensure you understand the "why" behind the solution.

**Part 3: Boilerplate Generation**
1. Use AI to generate a "Skeleton" for a new feature.
2. Example Prompt: "Generate a complete Express router for a 'Products' resource including GET, POST, and DELETE endpoints using Sequelize models."
3. Review the generated code. Notice if it uses variable names that match your existing codebase. This demonstrates the AI's understanding of your project's context.

**Part 4: Refactoring and Documentation**
1. Select a block of legacy code you wrote earlier in this roadmap (e.g., from Topic 002).
2. Ask the AI: "Refactor this code to use modern ES6 syntax (arrow functions, destructuring) and add JSDoc comments to every parameter."
3. Compare the original with the refactored version. Notice how the logic remains the same but the "Cleanliness" and "Readability" improve.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Hallucinated Libraries. AI models sometimes invent npm packages or API methods that don't actually exist. Always verify a new method in the official documentation before committing to it.
- **Gotcha 2:** Security Leaks. Be extremely careful when using public AI tools with company code. Never paste actual API keys, passwords, or sensitive customer data into an AI chat window.

### Reflection Question
How does AI-assisted coding fundamentally change the definition of a "Senior Engineer" compared to five years ago?