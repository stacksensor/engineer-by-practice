# Exercise 001 - Edge Computing Fundamentals

### Objective
Move execution closer to the user. Understand the paradigm shift from "Centralized Cloud" (e.g., AWS us-east-1) to **Edge Computing**. Learn how **Points of Presence (PoPs)** allow code to run in hundreds of data centers globally, reducing latency to milliseconds and eliminating the "speed of light" bottleneck.

### Core Concepts to Master
- **The Edge:** Computing that happens at or near the source of the data (the user).
- **PoP (Point of Presence):** A localized data center that is physically close to users.
- **Serverless at the Edge:** Lightweight execution environments (usually based on V8 Isolates rather than full VMs/Containers) like **Cloudflare Workers** or **Fastly Compute**.
- **Cold Start:** Why edge functions often have "zero" cold start compared to traditional Lambda functions.

### Research Topics
- "What is Edge Computing and why does it matter?"
- "The difference between Cloud and Edge"
- "V8 Isolates vs Containers for serverless"
- "Cloudflare Workers architecture"

---

### The Practical Challenge

**Part 1: The Speed of Light Test**
1. Ping a server in your local city. Note the latency (e.g., 5ms).
2. Ping a server on the other side of the world (e.g., from US to Australia). Note the latency (e.g., 250ms).
3. Calculate the time it takes for a user in Australia to interact with a centralized database in Virginia. 
4. Discuss: How does "The Edge" solve this?

**Part 2: Hello Edge (Cloudflare Workers)**
1. Create a free Cloudflare account.
2. Install the `wrangler` CLI.
3. Scaffold a new worker: `wrangler init hello-edge`.
4. Deploy the worker: `wrangler deploy`.
5. Access the URL from multiple locations (or use a service like `pingdom` or `uptrends`) and verify the fast response times globally.

**Part 3: Request Manipulation**
1. Update your worker to inspect the incoming `Request` headers.
2. If the user's country is "DE" (Germany), change the response language to German.
3. Research the `cf` object in Cloudflare Workers to see all the geographic data available at the edge.

**Part 4: Identifying the Limits**
1. Research the constraints of Edge Functions: CPU limits (e.g., 10ms-50ms), memory limits, and lack of traditional filesystem access.
2. Discuss: Why are these constraints necessary for running code at massive scale?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Database Trap." Running your code at the edge is fast, but if your code then has to talk to a database in Virginia, you've gained nothing. You must use "Edge-compatible" databases (like KV, Durable Objects, or Turso).
- **Gotcha 2:** Bundle Size. Edge platforms often have a limit on the size of your uploaded code (e.g., 1MB). You cannot simply import every library you want.

### Reflection Question
Why is Edge Computing essential for the "Next Billion Users" in regions with poor international internet connectivity?
