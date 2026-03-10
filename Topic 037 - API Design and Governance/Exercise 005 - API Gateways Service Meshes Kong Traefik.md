# Exercise 005 - API Gateways & Service Meshes (Kong / Traefik)

### Objective
One entry for all. Master the **API Gateway**—the single entry point for all your microservices. Learn how an API Gateway handles **Routing**, **Authentication**, **Rate Limiting**, and **Transformation** in a single place, so your actual service code can focus on "Business Logic." Compare this with the "Internal" security of a **Service Mesh** (e.g., Istio).

### Core Concepts to Master
- **API Gateway (North-South):** The traffic from the "Outside World" (Internet) to your servers. (Tools: Kong, Traefik, Tyk, AWS API Gateway).
- **Service Mesh (East-West):** The traffic between your "Internal Services" (e.g., Order to Inventory). (Tools: Istio, Linkerd).
- **Routing:** Directing `/users` to the User Service and `/orders` to the Order Service.
- **Middleware:** Adding a "Check if user is logged in" plugin to every request automatically.
- **Canary Releases:** Directing 5% of traffic to a new version of your API to test it "Live."

### Research Topics
- "The role of an API Gateway in microservices"
- "Kong Gateway Features: Auth, Rate-limiting, and Logging"
- "Traefik: The dynamic reverse proxy for Docker/K8s"
- "Service Mesh vs API Gateway: What's the difference?"

---

### The Practical Challenge

**Part 1: The Gateway Transformation**
1. You have 3 microservices: `Users`, `Orders`, `Payments`.
2. Draw a diagram of the user's path:
   - User -> `api.mycompany.com` (API Gateway) -> `Users/Orders/Payments`.
3. Discuss: Where should the "Login" logic happen? 
4. (Answer: The Gateway. It checks the token once and then tells the internal services "This user is Alex").

**Part 2: The Service Mesh (Concept)**
1. In a large system, the `Order Service` needs to talk to the `Payment Service`.
2. Discuss why using the "Public Gateway" for this internal talk is slow and insecure. 
3. Research how **Istio** adds a "Sidecar" to every service to handle encryption and retries between them.

**Part 3: Traefik's Dynamic Routing**
1. Research how **Traefik** uses labels in Docker to automatically "Find" a new service and create a URL for it.
2. Discuss why this is better than manually editing a config file every time you deploy a new app.

**Part 4: Identifying the "North-South" vs "East-West"**
1. Traffic from a user's mobile app: (Answer: North-South).
2. Traffic from the "E-mail Service" to the "User Database": (Answer: East-West).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Single Point of Failure. If the Gateway dies, your entire company is offline. You must run multiple Gateways behind a "Load Balancer."
- **Gotcha 2:** Latency Tax. Every request is being "Proxied" through the Gateway. If your Gateway is slow (or misconfigured), every single API call will feel lagged.

### Reflection Question
Why is it better to put "Global Rules" (like 'Allow only 1 request/sec from China') in an API Gateway instead of in your 100 individual microservices? (Answer: Consistency and centralized management).
