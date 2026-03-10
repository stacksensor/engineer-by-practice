# Exercise 002 - Prompt Engineering for Developers

### Objective
Learn to "Speak" to the model. Master the techniques of context-setting, roleplay, and few-shot prompting to extract high-quality, architecturally sound code from Large Language Models (LLMs).

### Core Concepts to Master
- **The System Prompt:** Setting the "Persona" (e.g., "You are a Senior Security Engineer") to guide the tone and complexity of the response.
- **Context Injection:** Providing the model with relevant schema definitions, file trees, or style guides so it doesn't have to guess.
- **Chain-of-Thought:** Asking the model to "Think step-by-step" before providing the final code, which significantly reduces logic errors.
- **Few-Shot Prompting:** Providing 2-3 examples of the desired output format to "tune" the model's behavior during the conversation.

### Research Topics
- "Prompt engineering techniques for developers"
- "What is Few-Shot prompting"
- "How to reduce LLM hallucinations in code"

---

### The Practical Challenge

**Part 1: The Persona Shift**
1. Prompt an AI with a generic request: "Write a React component for a data table."
2. Now, prompt it with a Role: "You are a Lead Frontend Architect obsessed with Accessibility and Performance. Write a React component for a data table using semantic HTML and memoization."
3. Compare the two outputs. Notice the use of `aria-labels`, `useMemo`, and a more robust structure in the second response.

**Part 2: Providing Context**
1. Prompt an AI to "Write a SQL query to find top users." It will fail because it doesn't know your schema.
2. Now, provide the Schema as context:
   ```text
   Schema:
   Table users: id, username
   Table orders: id, user_id, amount
   
   Prompt: Write an optimized SQL query to find the top 5 users by total order amount.
   ```
3. Observe how the output is now 100% accurate to your specific database structure.

**Part 3: Chain-of-Thought Debugging**
1. Give the AI a broken algorithm (e.g., a buggy Fibonacci function).
2. Use the instruction: "Analyze this function. First, explain the logic error. Second, provide the corrected code. Third, write three unit tests to verify the fix."
3. By forcing the model to "explain" first, it is much less likely to provide a "lazy" or incorrect fix.

**Part 4: Formatting and Few-Shot**
1. Task the AI with converting a list of raw terminal logs into a specific JSON structure.
2. Instead of just asking, provide one example:
   ```text
   Convert the following logs to JSON like this:
   "User logged in" -> { "event": "LOGIN", "status": "SUCCESS" }
   "Failed password" -> { "event": "LOGIN", "status": "FAILURE" }
   
   Logs:
   "Account locked"
   "User logged in"
   ...
   ```
3. Observe how the AI follows your pattern perfectly for the remaining logs.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Vague Request" Trap. Asking for "a website" or "an app" will result in generic, useless code. Be specific about technologies, libraries, and desired functionality.
- **Gotcha 2:** Length Constraints. Most LLMs have an output limit. If you ask for a 500-line file, it will likely cut off in the middle. Break your prompts down into smaller, modular components (e.g., "Write the Auth component", then "Write the UI layout").

### Reflection Question
How does prompt engineering enable developers to use specialized programming languages (like Rust or Go) even if they haven't fully mastered the syntax yet?