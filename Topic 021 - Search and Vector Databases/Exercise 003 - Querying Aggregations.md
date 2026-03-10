# Exercise 003 - Querying & Aggregations

### Objective
Master complex data retrieval. Learn how to use the **Query DSL (Domain Specific Language)** to build boolean queries that combine multiple search criteria, and use **Aggregations** to perform real-time data analysis (like finding the average price per category) across millions of documents.

### Core Concepts to Master
- **Leaf Queries:** Searching for specific values in specific fields (e.g., `match`, `term`, `range`).
- **Compound Queries:** Combining multiple queries using `bool` logic:
  - `must`: Must be true (affects score).
  - `filter`: Must be true (does NOT affect score, faster).
  - `should`: Like an OR, improves the score if true.
  - `must_not`: Must be false.
- **Aggregations (Aggs):** The "Group By" of the search world.
  - **Bucket Aggs:** Grouping documents into buckets (e.g., by category).
  - **Metric Aggs:** Calculating stats on those buckets (e.g., avg, sum, min, max).

### Research Topics
- "Elasticsearch bool query MUST vs FILTER"
- "Introduction to Elasticsearch Aggregations"
- "Building a faceted search UI"

---

### The Practical Challenge

**Part 1: The Boolean Search**
1. Index a group of documents with fields: `title`, `category`, `price`, `in_stock` (boolean).
2. Build a query that:
   - Matches "laptop" in the `title`.
   - Filters ONLY for `category: "electronics"`.
   - Filters ONLY for `price` less than 1000.
   - Must NOT be out of stock (`in_stock: true`).

**Part 2: The "Should" Boost**
1. Update your query to add a `should` clause for `brand: "Apple"`.
2. Observe how Apple-branded laptops move to the top of the search results while other laptops are still visible below them.

**Part 3: Basic Aggregations**
1. Use the `aggs` API to find the list of all unique categories in your index (`terms` aggregation).
2. Add a sub-aggregation to calculate the `avg` price for each of those categories.

**Part 4: Faceted Search (Conceptual)**
1. Research how modern e-commerce sites like Amazon use aggregations to build the "Sidebar Filters" (e.g., "Brands: Nike (12), Adidas (45)").
2. Discuss how you can run one single query that returns both the search results AND the counts for the sidebar filters at the same time.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Term Query on Text Fields. If you try to run a `term` query (exact match) on a `text` field, it will likely fail because the text field has been tokenized (e.g., lowercased). Use `match` for text, and `term` for keywords.
- **Gotcha 2:** Aggregation Memory. Running deep, nested aggregations on billions of documents can consume massive amounts of RAM and potentially crash an Elasticsearch node.

### Reflection Question
Why should you put "Price ranges" in the `filter` block of a boolean query instead of the `must` block?
