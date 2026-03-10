# Exercise 005 - Vector Databases (Pinecone / Milvus)

### Objective
Scale the "Nearest Neighbor" search. Learn how to use a specialized **Vector Database** (like **Pinecone**, **Milvus**, or **Weaviate**) to store millions of high-dimensional vectors and perform lightning-fast similarity searches that power AI recommendation engines and chatbots.

### Core Concepts to Master
- **HNSW (Hierarchical Navigable Small World):** One of the most common graph-based algorithms for fast "Approximate" nearest neighbor search.
- **Indexing vs. Storage:** Unlike a traditional DB, a Vector DB spends massive CPU effort on "Indexing" the space so that searching doesn't require comparing every single vector.
- **Metadata Filtering:** The ability to combine vector search with traditional filters (e.g., "Find documents similar to X, but only if they are from the 'Finance' category").
- **Upserting:** The process of inserting or updating a vector/document in the index.

### Research Topics
- "What is a Vector Database and why not just use Postgres?"
- "How Pinecone indexes work"
- "Comparing Milvus, Weaviate, and Pinecone"
- "Introduction to pgvector for Postgres"

---

### The Practical Challenge

**Part 1: The Cloud Index**
1. Create a free account on **Pinecone** (or set up a local **ChromaDB** or **Milvus** instance).
2. Create an index named `tutorial-index` with the correct dimension (e.g., 1536 if using OpenAI).
3. Ensure the metric is set to `cosine` or `euclidean`.

**Part 2: Preparing the Data**
1. Create a Python script.
2. Generate embeddings for a small list of sentences (e.g., "Documentation for Node.js", "Recipes for Italian Pasta", "How to fix a flat tire").
3. Create a unique ID for each.
4. Add Metadata: `{"category": "tech"}`, `{"category": "food"}`, etc.

**Part 1: The Upsert**
1. Format your data: `(id, vector, metadata)`.
2. Push the data to the index: `index.upsert(vectors=[...])`.

**Part 4: The Query**
1. Imagine a user asks: "How do I make spaghetti?"
2. Generate an embedding for that query.
3. Query the index: `index.query(vector=query_vector, top_k=2, include_metadata=True)`.
4. Observe the results. Which document has the highest score?
5. Now, run the same query but add a metadata filter to only include the `tech` category. Observe how the results change.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Dimension Mismatch. If your index is set for 768 dimensions but you try to upsert a 1536 vector, the DB will reject it. This is a common point of failure when switching embedding models.
- **Gotcha 2:** Accuracy vs Speed (ANN). Vector DBs use "Approximate" Nearest Neighbor (ANN) search. This means it might *occasionally* miss the absolute best result in exchange for being 1000x faster. Be aware of the "Recall" trade-off.

### Reflection Question
Why is a Vector Database essential for building applications that use "Generative AI" (like ChatGPT) on top of private company data?
