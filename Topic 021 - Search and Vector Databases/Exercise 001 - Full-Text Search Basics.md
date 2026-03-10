# Exercise 001 - Full-Text Search Basics (Elasticsearch)

### Objective
Go beyond `LIKE %query%`. Understand why traditional databases are slow for text search and learn the basics of **Elasticsearch** (part of the ELK stack) to build fast, relevant search experiences that support features like fuzziness, highlighting, and relevance scoring.

### Core Concepts to Master
- **Inverted Index:** The data structure that makes search fast by mapping words to the documents they appear in.
- **Documents & Indices:** In search, "Documents" are like rows and "Indices" are like tables.
- **The REST API:** Everything in Elasticsearch (creating, searching, deleting) is done via simple HTTP requests.
- **Relevance Scoring:** How Elasticsearch ranks search results using algorithms like BM25 to determine which document is the "best" match.

### Research Topics
- "What is an Inverted Index and how does it work?"
- "Elasticsearch vs traditional SQL search"
- "Installing Elasticsearch and Kibana with Docker"

---

### The Practical Challenge

**Part 1: The Local Search Engine**
1. Run Elasticsearch locally using Docker: `docker run -d -p 9200:9200 -e "discovery.type=single-node" elasticsearch:8.x`.
2. Verify it is alive: `curl localhost:9200`.

**Part 2: Indexing your first Document**
1. Use `curl` (or Postman) to index a document into an index named `books`:
   `curl -X POST "localhost:9200/books/_doc/1" -H 'Content-Type: application/json' -d '{"title": "The Art of Scalability", "author": "Abbott", "content": "A deep dive into distributed systems"}'`
2. Retrieve it: `curl localhost:9200/books/_doc/1`.

**Part 3: Basic Search**
1. Send multiple books to the index.
2. Perform a "Match" search for the word "Scalability": 
   `curl -X GET "localhost:9200/books/_search" -H 'Content-Type: application/json' -d '{"query": {"match": {"content": "scalability"}}}'`
3. Observe the `_score` field in the response.

**Part 4: Dealing with Typos (Fuzziness)**
1. Try searching for "Scalabilty" (with a typo). Note that the previous search likely returns 0 results.
2. Update your query to use `"fuzziness": "AUTO"`.
3. Run it again. Observe how Elasticsearch finds the correct document even with the typo.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Memory Usage. Elasticsearch (Java-based) is a memory hog. If your Docker container keeps crashing, you might need to increase the available RAM or set the `-e "ES_JAVA_OPTS=-Xms512m -Xmx512m"` heap size.
- **Gotcha 2:** Security Headers. Modern versions of Elasticsearch (8+) have security turned on by default. For local learning, you might need to disable SSL/Auth in the `elasticsearch.yml` to make simple `curl` commands work.

### Reflection Question
Why is a "Full-Text Search" engine usually separated from the "Primary Database" (Postgres/MySQL) in large-scale applications?
