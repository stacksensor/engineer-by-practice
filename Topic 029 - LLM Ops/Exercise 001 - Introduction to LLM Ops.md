# Exercise 001 - Introduction to LLM Ops

### Objective
From prompt to production. Understand the **LLM Ops** (Large Language Model Operations) lifecycle. Learn how running AI applications differs from traditional software (non-deterministic outputs, massive GPU requirements, and rapid model obsolescence), and explore the "Stack" required to manage models, data, and evals at scale.

### Core Concepts to Master
- **The LLM Ops Loop:** Data Curation -> Training/Fine-tuning -> Evaluation -> Deployment -> Monitoring.
- **Foundational Models (FM) vs. Fine-tuned Models:** When to use GPT-4 as-is vs. when to build your own.
- **Tokens & Context Windows:** Understanding the "Currency" of LLMs and the physical limits of how much information they can process at once.
- **Inference vs. Training:** The difference between "using" a model (low cost) and "building/teaching" a model (high cost).

### Research Topics
- "What is LLM Ops? (Fiddler AI, Weights & Biases)"
- "The LLM Application Stack (LangChain, LlamaIndex, Pinecone)"
- "Differences between DevOps, MLOps, and LLMOps"

---

### The Practical Challenge

**Part 1: The Token Lab**
1. Use a tool like **OpenAI's Tokenizer** (or `tiktoken` in Python).
2. Input 3 sentences:
   - "Hello, my name is Alex."
   - "A quick brown fox jumps over the lazy dog."
   - "你好，我叫亚历克斯。" (Chinese)
3. Observe how many "Tokens" each sentence uses. 
4. Discuss: Why are some languages "More expensive" to process than others?

**Part 2: Managing Model Versions**
1. Research how models like **Llama-3** or **Mistral** are versioned (e.g., `instruct`, `base`, `8B`, `70B`).
2. If you find a perfect prompt for `Llama-3-8B`, will it automatically work for `Llama-3-70B`? 
3. Discuss the importance of a "Prompt Management" tool (like LangSmith or Portkey).

**Part 3: The Determinism Problem**
1. Run a request to an LLM with `temperature=0.0` and again with `temperature=1.0`. 
2. Record the outputs 5 times for each.
3. Observe how 0.0 is "Consistent" (mostly) and 1.0 is "Creative." 
4. Discuss: Why does this make traditional "Unit Testing" (checking for an exact string) very difficult?

**Part 4: Identifying the "Moat"**
1. Discuss: If everyone is using the same GPT-4 API, what makes one company's AI product better than another's? (Answer: Data, Evals, and fine-tuning).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Context Overflow. If your user inputs a 50-page document into a context window that only supports 10 pages, the model will "Forget" the start of the data. You must handle "Chunking" and "Summarization."
- **Gotcha 2:** The "Cost Spike." An LLM API is a "Black hole" for money if you don't set rate limits. One buggy loop could cost $5,000 in an hour.

### Reflection Question
Why is "Data Curation" the most important job in LLM Ops, even more than the model choice?
