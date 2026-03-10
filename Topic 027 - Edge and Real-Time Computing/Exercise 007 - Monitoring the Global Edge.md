# Exercise 007 - Monitoring the Global Edge

### Objective
Observe the world. Learn how to monitor and debug applications that are running in 300+ locations simultaneously. Master the use of **Synthetic Monitoring**, **Log Tailing at Scale**, and **Global Performance Dashboards** to identify when a specific region (e.g., Brazil or India) is having a localized outage or a slow connection to your origin.

### Core Concepts to Master
- **Synthetic Monitoring:** Using bots to "Simulate" a user visiting your site from specific cities (London, Tokyo, NYC) every minute.
- **Log Aggregation:** How to pull logs from all edge nodes back into a central place for analysis.
- **Tail-Latency (p99):** Why looking at "Average" latency is useless in a global system (e.g., your site is fast in the US but 10 seconds slow in Africa).
- **Core Web Vitals:** Measuring the real-user experience (LCP, FID, CLS) across different geographic segments.

### Research Topics
- "Global uptime monitoring tools"
- "Monitoring Cloudflare Workers with Grafana or Logpush"
- "What is RUM (Real User Monitoring)?"
- "Analyzing edge logs with BigQuery"

---

### The Practical Challenge

**Part 1: The Multi-Region Ping**
1. Use a tool like `ping.pe` or `uptrends` to check the response time of your edge worker from 20 different cities.
2. Identify the "Slowest" city. 
3. Research why that city is slow (Is it far from a PoP? Is there a fiber optic break?).

**Part 2: Log Tailing at the Edge**
1. Research how to use `wrangler tail` (Cloudflare) to see real-time logs from your global workers.
2. Invoke your worker from a VPN in a different country.
3. Observe how the logs show the "Data Center" ID (e.g., `LHR` for London, `SFO` for San Francisco).

**Part 3: The Dashboard Design**
1. Sketch a "Global Health Dashboard." 
2. What metrics would you include? (e.g., Error rate per region, p95 latency per region, Cache Hit ratio).
3. If you see a spike in errors ONLY in the `EZE` (Buenos Aires) data center, what would be your first troubleshooting step?

**Part 4: Core Web Vitals at Scale**
1. Research how the Chrome User Experience Report (CrUX) works.
2. Discuss why a "Fast" edge response doesn't always lead to a "Fast" user experience if your JavaScript is too heavy or your images are too large.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Sampling" bias. If you have 100 million requests, you cannot store every single log. You must use "Sampling" (only storing 1% of logs). If a bug only affects a few users, you might miss it entirely in your logs!
- **Gotcha 2:** Monitoring the Monitor. If your monitoring service goes down, you are blind to your own production status. High-reliability teams often use two independent monitoring providers.

### Reflection Question
How does "Observability" differ from "Monitoring" in the context of a globally distributed edge system?
