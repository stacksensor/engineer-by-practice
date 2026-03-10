# Exercise 005 - Load Balancing Strategies (L4 vs L7)

### Objective
Distribute the load effectively. Master the difference between **Layer 4 (Transport)** and **Layer 7 (Application)** Load Balancing. Learn how "Least Connection," "Round Robin," and "IP Hashing" algorithms work, and understand when to use an "In-Cluster" Balancer vs. a "Global" Cloud Balancer.

### Core Concepts to Master
- **Layer 4 (TCP/UDP):** Balancing based on IP and Port. Fast, but "blind" to the content of the request.
- **Layer 7 (HTTP/HTTPS):** Balancing based on URLs, Headers, or Cookies. Slower (requires SSL termination) but highly intelligent.
- **Session Persistence (Sticky Sessions):** Ensuring a user stays connected to the same server (important for legacy apps with local state).
- **Health Checks:** How the balancer detects a dead server and removes it from the pool.

### Research Topics
- "L4 vs L7 Load Balancing for developers"
- "NGINX load balancing algorithms"
- "Global Server Load Balancing (GSLB) vs Local Balancers"

---

### The Practical Challenge

**Part 1: The NGINX Balancer**
1. Set up 3 identical "Backend" servers (simple web apps that return their own hostname).
2. Set up an **NGINX** instance as a Load Balancer in front of them.
3. Use the `upstream` block to define your servers. 
4. Verify "Round Robin" behavior by refreshing your browser multiple times.

**Part 2: Content-Based Routing (L7)**
1. Update your NGINX config to use different backends based on the URL path:
   - `/api` -> Sent to Team A's cluster.
   - `/images` -> Sent to a Static Asset cluster.
2. Discuss why a Layer 4 (IP-only) balancer cannot do this.

**Part 3: Sticky Sessions**
1. Research how to use "Cookie-based" affinity in NGINX or AWS ALB.
2. Discuss: Why does this make horizontal scaling harder to manage?

**Part 4: The Health Check**
1. Define a `/health` endpoint on your backend servers.
2. Intentionally make one server return a `500 Internal Server Error`.
3. Observe how the Load Balancer automatically stops sending traffic to that server until it becomes healthy again.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The Single Point of Failure. If you only have one Load Balancer, and it crashes, your entire system is down. In production, you need "High Availability" balancers using techniques like `Keepalived` or cloud native services (AWS ELB).
- **Gotcha 2:** X-Forwarded-For. Because the Load Balancer acts as a proxy, your backend servers will see the Load Balancer's IP as the "Client IP." You must configure the balancer to pass the original IP in the `X-Forwarded-For` header.

### Reflection Question
Why would you choose a Layer 4 Load Balancer for a high-traffic gaming server but a Layer 7 Load Balancer for an e-commerce website?
