# Exercise 002 - Model Evaluation (Evals)

### Objective
Measure the "Smartness." Master the art of **Model Evaluation (Evals)**. Learn how to move away from "Vibe Checks" (reading a few outputs and deciding they look good) to automated, rigorous testing. Learn how to use **LLM-as-a-Judge**, **Ground Truth datasets**, and metrics like **Faithfulness** and **Relevancy**.

### Core Concepts to Master
- **Benchmark Datasets:** MMLU, GSM8K, HumanEval (standard tests for general knowledge or coding).
- **Golden Dataset:** A hand-curated set of 50-100 "Input/Output" pairs that represent the perfect behavior for YOUR specific app.
- **LLM-as-a-Judge:** Using a powerful model (like GPT-4) to grade the outputs of a smaller, faster model (like Llama-3-8B).
- **RAG Metrics (The RAGAS framework):** 
  - **Faithfulness:** Does the answer match the retrieved context?
  - **Answer Relevancy:** Does the answer actually respond to the user's question?

### Research Topics
- "How to build an evaluation pipeline for LLMs"
- "Using RAGAS for evaluating RAG applications"
- "What is a 'Vibe Check' in AI engineering?"
- "The DeepEval framework"

---

### The Practical Challenge

**Part 1: The Manual "Golden" Set**
1. Create a JSON file with 5 "Questions" related to a hypothetical product (e.g., "A subscription coffee app").
2. Manually write the "Expected Perfect Answer" for each.
3. This is your "Ground Truth."

**Part 2: The LLM Judge**
1. Send the 5 questions to a small model (e.g., GPT-3.5 or Llama-3-8B).
2. Take the 5 "Small outputs."
3. Send a prompt to a large model (GPT-4o/Claude 3.5):
   - "Here is an Expected Answer and a Student Answer. Grade the Student on a scale of 1-5 for accuracy. Explain your reasoning."
4. Observe if the "Judge" correctly identifies errors in the smaller model's logic.

**Part 3: Testing for Hallucinations**
1. Intentionally provide an LLM with "False Context" (e.g., "The capital of France is London").
2. Ask it: "What is the capital of France?". 
3. If it answers "London," it is being "Faithful" but "Factually Wrong." 
4. If it answers "Paris," it is "Hallucinating" relative to the context provided.
5. Discuss which behavior is better for a customer support bot.

**Part 4: Continuous Evals**
1. Research how to integrate Evals into a **CI/CD pipeline**. 
2. Discuss: If a developer updates the prompt, and the Eval score drops from 95% to 80%, should the code be allowed to move to production?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "The Judge is Biased." Large models tend to prefer their own writing style. They also tend to give higher scores to "Polite" but "Correct" answers.
- **Gotcha 2:** High Cost of Evals. If you have 1,000 eval questions and you run them twice a day using GPT-4, you will spend $100/day just on testing. Use "Sampling" or smaller models for routine testing.

### Reflection Question
Why is a "Poorly defined Eval" more dangerous than the LLM making a mistake?
