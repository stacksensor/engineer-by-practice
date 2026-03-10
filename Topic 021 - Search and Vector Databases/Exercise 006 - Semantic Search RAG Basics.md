# Exercise 006 - Semantic Search & RAG Basics

### Objective
Build the modern AI stack. Implement **Retrieval Augmented Generation (RAG)**—the architecture that allows LLMs (like GPT-4) to answer questions based on a specific, private knowledge base without retraining the model.

### Core Concepts to Master
- **The Context Window:** Large Language Models have a limit on how much text they can "read" at once.
- **The RAG Pipeline:**
  1. **User Query:** User asks a question.
  2. **Retrieval:** Convert the query to a vector, search the Vector DB for the most relevant documents.
  3. **Augmentation:** Combine the user question + the retrieved documents into a single "Super Prompt."
  4. **Generation:** Ask the LLM to "Answer the question based ONLY on the provided context."
- **Hallucination Prevention:** How RAG reduces the chance of the AI making things up by grounding its answers in real data.

### Research Topics
- "What is Retrieval Augmented Generation (RAG)?"
- "Building a chatbot with LangChain and Pinecone"
- "Token limits and prompt engineering for RAG"

---

### The Practical Challenge

**Part 1: The Search-as-Knowledge step**
1. Take your setup from Exercise 005.
2. Imagine the user asks: "What should I do if I get a flat tire?"
3. Retrieve the top 3 relevant text snippets from your Vector DB.

**Part 2: Designing the "System Prompt"**
1. Create a variable `context` containing the text from those 3 snippets.
2. Write a prompt: 
   `You are a helpful assistant. Answer the user question based only on this context: {context}. If the answer is not in the context, say 'I don't know'. User Question: {question}`
3. Discuss: Why is the "If the answer is not in the context..." part so important?

**Part 3: The Generation step**
1. (Conceptual or Code): Send this prompt to an LLM API (OpenAI/Anthropic).
2. Compare the AI's response to the original text snippets. Note how the AI summarizes and reformats the search results to be more conversational.

**Part 4: Handling Long Documents (Chunking)**
1. Research "Chunking Strategies."
2. If you have a 10,000-word document, why can't you just embed the whole thing into one vector?
3. Discuss the pros and cons of "Fixed-size chunking" vs "Semantic chunking" (breaking by paragraph/heading).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Context Stuffing. If you retrieve 50 documents and try to put them all in the prompt, you might exceed the LLM's token limit or confuse the model (the "Lost in the Middle" problem).
- **Gotcha 2:** Relevance is not Truth. If your Vector DB returns a document that is *wrong*, the AI will confidently give a *wrong* answer. "Garbage In, Garbage Out."

### Reflection Question
How does RAG solve the problem of "Data Freshness" (where an LLM's training data might be 1-2 years out of date)?
