# Exercise 003 - Metrics & Dashboards (Prometheus/Grafana)

### Objective
Visualize the "Health" of your system. Move from logging *events* to monitoring *metrics* (CPU usage, RAM, Response Latency, Throughput). Implement Prometheus to scrape data from your servers and Grafana to build professional real-time monitoring dashboards.

### Core Concepts to Master
- **Metrics vs Logs:** Logs tell you *what* happened; Metrics tell you *how* the system is performing (Numbers over time).
- **The Prometheus Scraper:** A system that periodically "pulls" numeric data from an endpoint (e.g., `/metrics`) on your server.
- **Grafana Dashboards:** A visualization engine used to create line charts, gauges, and alerts based on metric data.
- **Counter vs Gauge:** 
  - **Counter:** A value that only goes up (e.g., total requests handled).
  - **Gauge:** A value that can go up or down (e.g., current CPU usage).

### Research Topics
- "Prometheus vs ELK: When to use which?"
- "Monitoring Node.js with prom-client"
- "Standard SRE metrics (The Four Golden Signals)"
- "Building a Grafana dashboard for Express"

---

### The Practical Challenge

**Part 1: The Metrics Endpoint**
1. In your Node.js app, install the `prom-client` library.
2. Initialize the client and expose a specialized route: `GET /metrics`.
3. Visist the route in your browser. You should see a list of raw numeric values (CPU, memory, etc.) in a specific "Prometheus Format."
4. Add a custom "Counter" for every time a specific API endpoint is called.

**Part 2: The Prometheus Collector**
1. Launch Prometheus using Docker: `docker run -p 9090:9090 -v ./prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus`.
2. Configure `prometheus.yml` to "scrape" your local application every 5 seconds.
3. Open the Prometheus UI (`http://localhost:9090`). Write your first query to see the CPU usage of your app.

**Part 3: The Grafana Visualization**
1. Launch Grafana using Docker: `docker run -d -p 3000:3000 grafana/grafana`.
2. Login (`admin/admin`) and add your Prometheus instance as a "Data Source."
3. Create a new Dashboard. 
4. Add a graph showing "Total Requests per Minute." Use the `rate()` function in Prometheus's query language (PromQL).

**Part 4: The Alerting Fire**
1. Configure an Alert in Grafana.
2. Rule: "If the 95th Percentile Latency is > 500ms for more than 2 minutes, trigger an alert."
3. Simulate high latency in your app (use a `setTimeout` for a random 1 second in a route).
4. Watch the alert turn from "Green" to "Red" in the dashboard. This is how SREs (Site Reliability Engineers) know when to wake up.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Cardinality Explosion. Never use a "User ID" as a label for a metric (e.g., `requests_total{user_id="123"}`). This creates a new metric for every user, which will crash your Prometheus server and use infinite RAM.
- **Gotcha 2:** Pull vs Push. Prometheus "Pulls" data. If your server is behind a firewall, it cannot be reached by the scraper. You may need a "Pushgateway" for short-lived tasks like Lambda functions.

### Reflection Question
What are the "Four Golden Signals" of monitoring, and why are they considered the most important metrics for any web system?
