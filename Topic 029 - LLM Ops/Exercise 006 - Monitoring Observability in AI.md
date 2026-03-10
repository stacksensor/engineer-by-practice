# Exercise 006 - Monitoring & Observability in AI

### Objective
Debug the "Black Box." Master **LLM Observability**. Learn how to track and visualize the inner workings of your AI app using tools like **LangSmith**, **HoneyHive**, or **Arize Phoenix**. Learn how to monitor "Semantic Drift," "Hallucination Rates," and "Cost per User" in real-time.

### Core Concepts to Master
- **Tracing:** Visualizing the multi-step "Chain" of an AI request (e.g., User -> Search -> Retrieval -> Prompt -> Answer).
- **Sentiment & Vibe Monitoring:** Tracking if the model's outputs are becoming "more frustrated" or "less helpful" over time.
- **Cost Tracking:** Associating every token used with a specific user or API key.
- **Feedback Loops:** Collecting "Thumb Ups/Down" from users and using that data to improve your Eval sets.

### Research Topics
- "Traces and Spans in LLM applications"
- "Monitoring for Hallucinations in production"
- "Arize Phoenix: Open-source observability for LLMs"
- "Tracking user feedback (Thumbs up/down) in LangChain"

---

### The Practical Challenge

**Part 1: The Trace Visualization**
1. Research the **LangSmith** UI (or a similar tool).
2. Imagine a RAG application. 
3. Draw/Trace the steps:
   - User Input.
   - Vector Search Query.
   - Top 3 Results (The Context).
   - The Final Prompt sent to the LLM.
   - The LLM Response.
4. Discuss: If the answer is "I don't know," where do you look in the trace to find the failure? (Answer: Was the search query bad? Or was the context missing the info?).

**Part 2: Cost Attribution**
1. Design a system that calculates cost per request.
2. If `tokens_input` cost $0.05 per 1k and `tokens_output` cost $0.10 per 1k.
3. Track the total cost of a user's session.
4. Discuss: How do you identify "Toxic" users who are intentionally trying to drain your API budget?

**Part 3: Hallucination Detection (Real-time)**
1. Research the "Self-Consistency" check.
2. Ask the same question to the LLM 3 times. If you get 3 different answers, the hallucination risk is "High."
3. Discuss how to log this "Disagreement" in your observability dashboard.

**Part 4: The Feedback API**
1. Write a schema for a "Feedback" event: `{request_id, user_id, rating: 1|0, comment: "too long"}`.
2. Discuss how these "Negative Feedback" events become the "Test Cases" for next week's Prompt Engineering session.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Privacy in Logs. Tracing tools often store every prompt and answer. If your users are inputting passwords or private health data, your "Observability" tool just became a major security leak.
- **Gotcha 2:** The "Storage" Bill. Detailed tracing of every request uses a lot of disk space. For high-volume apps, only trace a "Sample" (e.g., 5%) of standard requests but 100% of errors.

### Reflection Question
How does "Tracing" solve the problem where an engineer says "It works locally on my machine" but the AI fails in production?
