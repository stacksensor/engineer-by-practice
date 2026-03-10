# Exercise 002 - Centralized Logging (ELK Stack)

### Objective
Unify your server logs. Move from checking individual text files on a server to a centralized logging system (like the ELK Stack: Elasticsearch, Logstash, Kibana) that allows you to search, filter, and visualize millions of log lines across all your microservices from a single dashboard.

### Core Concepts to Master
- **Structured Logging:** Logging data as JSON objects (e.g., `{"level": "info", "user": 1}`) rather than plain text strings so they can be easily parsed and searched.
- **Elasticsearch:** A powerful search engine that indexes and stores your log data.
- **Logstash / Fluentd:** The "Ingestion" layer that collects logs from your servers and sends them to Elasticsearch.
- **Kibana:** The "Visualizer" where you write queries and build charts (e.g., "HTTP requests over time").

### Research Topics
- "What is the ELK stack?"
- "Winston vs Bunyan for Node.js logging"
- "Structured logging best practices"
- "Using Kibana to filter logs"

---

### The Practical Challenge

**Part 1: Structured Logging with Winston**
1. In your Node.js application, install the `winston` library.
2. Replace all `console.log` calls with standard Winston levels: `logger.info()`, `logger.warn()`, `logger.error()`.
3. Configure Winston to output in **JSON format**.
4. Observe the log output: `{"message": "Server started", "level": "info", "timestamp": "..."}`. This is now "Machine Readable."

**Part 2: The Logic of Aggregation**
1. Launch the ELK stack using Docker. 
   *(Self-Correction: ELK is heavy for a local machine. For this exercise, you may also use a lightweight alternative like **Grafana Loki** or a cloud log tool like **BetterStack**).*
2. Configure your Logger to send data via HTTP to your centralized logging server instead of just the console.
3. Verify that new events appear in the web dashboard.

**Part 3: The Power of Search**
1. Generate several hundred logs with different "Meta Data" (e.g., unique User IDs, different API routes).
2. Open the Kibana (or Loki) dashboard.
3. Write a query to find ONLY logs where the `level` is `error` and the `route` starts with `/api/payments`.
4. Imagine doing this with `grep` across 50 different servers—you just saved hours of work.

**Part 4: Visualizing Failure**
1. Create a simple "Histogram" chart in your dashboard.
2. Plot the number of `404 Not Found` logs per minute.
3. Observe the chart. If you suddenly see a spike in 404s, it likely means a recent deployment broke a major link or a bot is attempting to scan your site for vulnerabilities. This is "Observability."

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** PII Leaks. Log files are often kept for years. Never log "Personally Identifiable Information" (PII) like names, phone numbers, or passwords.
- **Gotcha 2:** Disk Overflow. If your logs are too verbose (e.g., logging every SQL query), you will fill up your server's disk space. Always implement "Log Rotation" to delete or archive old logs automatically.

### Reflection Question
Why is "Structured Logging" (JSON) considered vastly superior to "Plain Text Logging" for large-scale application debugging?
