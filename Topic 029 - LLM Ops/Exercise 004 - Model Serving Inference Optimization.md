# Exercise 004 - Model Serving & Inference Optimization

### Objective
Deploy at the speed of thought. Master high-performance **Model Serving**. Learn how to use inference engines like **vLLM**, **TGI (Text Generation Inference)**, or **Ollama** to serve open-source models with low latency. Understand **Continuous Batching**, **KV Caching**, and how to scale your GPU cluster.

### Core Concepts to Master
- **Continuous Batching:** Processing multiple user requests at once even if they start at different times.
- **KV (Key-Value) Cache:** Storing the "Mathematical state" of the earlier tokens so the model doesn't have to re-calculate them for every new word it generates.
- **Speculative Decoding:** Using a tiny, fast model to "Guess" the next few words and a large model to "Verify" them.
- **vLLM PagedAttention:** How vLLM manages GPU memory similar to traditional "Virtual Memory" to allow more users on a single GPU.

### Research Topics
- "vLLM: Easy, fast, and cheap LLM serving"
- "Continuous batching vs Static batching"
- "Optimizing LLM inference latency"
- "Running models on CPU with llama.cpp GGUF"

---

### The Practical Challenge

**Part 1: Running Model Locally (Ollama/llama.cpp)**
1. Install **Ollama** on your machine.
2. Run a model: `ollama run llama3`.
3. Observe the "Time to First Token" and "Tokens per second."
4. Use `top` or `Activity Monitor` to see how much RAM/GPU memory it's using.

**Part 2: KV Cache Visualization (Conceptual)**
1. Imagine an LLM is generating a story word-by-word.
2. Without a KV Cache, to generate word #10, the model must re-read words #1-9.
3. Draw a diagram showing how the KV Cache saves time as the generation gets longer.

**Part 3: Throughput vs. Latency**
1. Research the trade-off in **vLLM**. 
2. If you serve 10 users at once, they might each get 5 tokens/second (High Throughput).
3. If you serve 1 user at once, they might get 50 tokens/second (Low Latency).
4. Discuss: Which setting is better for a "Chatbot" vs. an "Offline Document Summarizer"?

**Part 4: Quantization Formats**
1. Research the difference between **AWQ**, **GPTQ**, and **GGUF**.
2. Discuss why a "4-bit" model is almost 4x smaller than a "16-bit" model but only ~1-2% less "Smart."

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Out-of-Memory (OOM). LLMs are memory-hungry. If your model needs 12GB and your GPU only has 8GB, it will crash or run 100x slower on the CPU.
- **Gotcha 2:** The "Token" Cliff. As a chat gets longer, the KV Cache grows. Eventually, it hits the GPU's memory limit and the model becomes extremely slow or starts "forgetting."

### Reflection Question
How does using an inference engine like vLLM help a company reduce their cloud bill by 2x-5x compared to standard naive model serving?
