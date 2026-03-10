# Exercise 007 - From Experiment to Infrastructure

### Objective
Scale the magic. Master the architectural patterns for moving an "AI Prototype" (a messy Jupyter notebook) into a robust "AI Service." Learn about **Asynchronous Inference**, **Model Chaining**, **Agentic Workflows**, and how to prepare your infrastructure for a future where models change every 6 months.

### Core Concepts to Master
- **The "Async" AI Pattern:** Letting the user know "We are processing your request" while the 30-second AI task runs in the background.
- **Model Chaining:** Using a small, cheap model to "Screen" a request before sending it to a large, expensive model.
- **Agentic Workflows:** Systems that can "Use Tools" (search the web, run code, query DB) to solve a problem.
- **Feature Flags for Models:** Using Blue/Green deployments to gradually move traffic from `gpt-4` to `gpt-4o`.

### Research Topics
- "Building production-grade AI agents"
- "The Router pattern in LLM applications"
- "Using Redis/Celery for async LLM processing"
- "AI infrastructure: Designing for model swap-ability"

---

### The Practical Challenge

**Part 1: The "Router" Architecture**
1. Imagine an app that does two things:
   - Task A: "Check my grammar" (Easy).
   - Task B: "Write a 10-page legal contract" (Hard).
2. Design a "Router" service that:
   - Uses a tiny, fast model (like Llama-3-8B) to classify the request.
   - If Task A -> Use a cheap model.
   - If Task B -> Use an expensive model.
3. Calculate the potential savings for a company with 1 million requests/day.

**Part 2: The Async User Interface**
1. Design a WebSocket or Webhook workflow for an AI Image Generator.
2. Step 1: User sends prompt. Server replies "ID: 123, Status: Pending."
3. Step 2: Server adds task to a **Redis Queue**.
4. Step 3: A "Worker" processes the image on a GPU (takes 10 seconds).
5. Step 4: Worker pings the Frontend via WebSocket: "Task 123 is ready!".
6. Discuss: Why is this better than having the user's browser wait for a 10-second HTTP response?

**Part 3: The "Model Swap" Ready API**
1. Write a wrapper class/function that abstracts the LLM provider.
2. Instead of calling `openai.chat()`, your code calls `MyAI.generate()`.
3. Discuss how this allowed companies to switch from OpenAI to Anthropic (Claude) in 1 hour when OpenAI had an outage.

**Part 4: Designing for "Continuous Improvement"**
1. Research how to setup a "Feedback Loop" where the 1% most "Poorly rated" responses are automatically sent to a human labeling team for review.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-Agenting. Giving an AI "Full control" of your system usually results in infinite loops and high bills. Always start with "Human-in-the-loop" or "Deterministic Workflows."
- **Gotcha 2:** The "Version" Trap. If you hardcode `gpt-4-0314` in your code, your app will break when that specific version is deprecated by the provider. Use aliases or environment variables.

### Reflection Question
How does the "AI Engineering" role bridge the gap between "Traditional Software Engineering" and "Data Science"?
