# Exercise 003 - Fine-tuning Basics & PEFT (LoRA)

### Objective
Teach old models new tricks. Master the concepts of **Fine-tuning**. Learn why you shouldn't train a model from scratch, and instead use **PEFT (Parameter-Efficient Fine-Tuning)** techniques like **LoRA (Low-Rank Adaptation)**. Learn how to transform a general-purpose model into a specialist that understands your company's unique jargon and style.

### Core Concepts to Master
- **Full Fine-tuning:** Updating every single billion-parameter of a model (very expensive).
- **LoRA (Low-Rank Adaptation):** Only training a tiny "Adapter" layer while keeping the main model frozen.
- **Quantization (QLoRA):** Reducing the precision of the model (e.g., from 16-bit to 4-bit) so it fits on cheaper consumer-grade GPUs.
- **Instruct Tuning:** Fine-tuning a model specifically to follow commands (Question -> Answer) vs. "Base" tuning (Text -> More Text).

### Research Topics
- "LoRA: Low-Rank Adaptation of Large Language Models (Original Paper)"
- "Fine-tuning Llama-3 with the Unsloth library"
- "When to use RAG vs when to use Fine-tuning"
- "Datasets for fine-tuning: JSONL formatting"

---

### The Practical Challenge

**Part 1: Preparing the Dataset**
1. Research the **JSONL** format required by most fine-tuning libraries (e.g., `{"prompt": "...", "completion": "..."}`).
2. Create a "Dataset" of 10 examples that teach a model how to answer in a very specific persona (e.g., "The Pirate Customer Support bot").

**Part 2: The LoRA Concept (Conceptual)**
1. Imagine a model is a giant library of 7 billion books.
2. Discuss why it's faster to write a 10-page "Guide" (LoRA) that tells the librarian how to search the books, rather than re-writing all 7 billion books.

**Part 3: Tooling Exploration**
1. Research tools like **Unsloth** or **Axolotl**. 
2. Look at a YAML configuration file for one of these tools. 
3. Identify settings for `rank` (usually 8, 16, or 32) and `alpha`.
4. Discuss: How does the "Rank" affect the "Intelligence" vs "Memory Usage" of the fine-tune?

**Part 4: The Merge**
1. Research how to "Merge" a LoRA adapter back into the base model.
2. Discuss why you might want to keep the adapter separate (multiple adapters for one model) vs. merging it (better performance, easier to serve).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Catastrophic Forgetting. If you over-train a model on Pirate talk, it might forget how to do basic math or follow other safety instructions. Balance your dataset!
- **Gotcha 2:** Data Quality. "Garbage in, Garbage out." If your fine-tuning data contains typos and wrong answers, the model will learn to incorporate those typos.

### Reflection Question
If Fine-tuning is so powerful, why is RAG (Retrieval Augmented Generation) still the preferred method for dealing with "Frequently changing data" (like today's news or inventory counts)?
