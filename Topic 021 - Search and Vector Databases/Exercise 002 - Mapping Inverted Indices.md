# Exercise 002 - Mapping & Inverted Indices

### Objective
Define the shape of your data. Learn how to use **Mappings** to tell Elasticsearch exactly how to treat each field (e.g., as searchable text, a raw keyword, or a date), and understand how the "Analysis Pipeline" (Tokenizers and Filters) transforms your raw text into a searchable inverted index.

### Core Concepts to Master
- **Mapping:** The schema definition in Elasticsearch.
- **Text vs. Keyword:** 
  - `text` is analyzed and broken into tokens (used for search).
  - `keyword` is stored exactly as-is (used for filtering and sorting).
- **Analysis Pipeline:**
  - **Character Filters:** Stripping HTML or cleaning text.
  - **Tokenizer:** Breaking a string into individual words (e.g., "Standard Tokenizer").
  - **Token Filters:** Converting to lowercase, removing "stop words" (a, an, the), or Stemming (changing "running" to "run").
- **Dynamic Mapping:** How Elasticsearch automatically guesses types (and why you should avoid it in production).

### Research Topics
- "Elasticsearch mapping types: text vs keyword"
- "Understanding the Standard Analyzer"
- "What is Stemming and Lemmatization?"

---

### The Practical Challenge

**Part 1: The Analysis Lab**
1. Use the `_analyze` API to see how the standard analyzer breaks down a sentence:
   `GET /_analyze { "analyzer": "standard", "text": "The 2 Quick-brown foxes jumped!" }`
2. Observe the generated tokens. Notice how punctuation is gone and words are lowercased.

**Part 2: Creating a Strict Mapping**
1. Create a new index `products` with an explicit mapping:
   - `name`: `text` (for search).
   - `category`: `keyword` (for exact filters).
   - `price`: `double`.
   - `created_at`: `date`.
2. Try to index a document where the `price` is a string "FREE". Observe the error as Elasticsearch enforces your schema.

**Part 3: Custom Analyzers**
1. Research how to create an analyzer that removes "Stop Words" (common words like 'and', 'or', 'the').
2. Apply this analyzer to a new index. 
3. Index the sentence "To be or not to be" and run an analysis. Notice how the tokens are almost empty!

**Part 4: The Inverted Index Visual**
1. Sketch an Inverted Index for these 3 sentences:
   - Doc 1: "I love coding"
   - Doc 2: "Coding is fun"
   - Doc 3: "I love fun"
2. Your sketch should look like a table: Word -> [List of Doc IDs].

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Changing Mappings. You cannot change a field's type (e.g., from `text` to `keyword`) after it has been created. You must create a new index and "Reindex" the data.
- **Gotcha 2:** Field Collisions. If you have two different types of data (e.g., a "User" object and a "Product" object) in the same index, their fields must have the same types or they will conflict.

### Reflection Question
Why would you set a `user_email` field to the `keyword` type instead of the `text` type?
