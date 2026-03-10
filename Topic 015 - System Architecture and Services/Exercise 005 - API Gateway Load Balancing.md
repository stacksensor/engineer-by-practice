# Exercise 005 - API Gateway & Load Balancing

### Objective
Manage traffic at scale. Implement an API Gateway to provide a single, secure entry point for your multiple microservices, and explore Load Balancing techniques to distribute user requests across multiple server instances to ensure high availability and prevent single-point failures.

### Core Concepts to Master
- **API Gateway:** The "Traffic Cop" of your architecture. It handles routing, authentication, and rate-limiting for all your services.
- **Reverse Proxy (Nginx/Kong):** A server that sits in front of your web servers and forwards client requests to the appropriate backend service.
- **Round-Robin Load Balancing:** The simplest algorithm where requests are sent to servers in a sequential circle (Server A, then B, then C).
- **Health Checks:** The load balancer's ability to "ping" a server and automatically stop sending traffic to it if it is unresponsive.

### Research Topics
- "What is an API Gateway?"
- "Nginx as a load balancer tutorial"
- "Difference between L4 and L7 load balancing"
- "Rate limiting and throttling at the gateway level"

---

### The Practical Challenge

**Part 1: The Multi-Server Simulation**
1. Create two identical Express apps: `Server A` (port 3001) and `Server B` (port 3002).
2. Have each one return a message indicating which server it is: `{"server": "A"}`.
3. Start both servers.

**Part 2: The Nginx Proxy**
1. Launch an Nginx container using Docker.
2. Configure a `default.conf` to act as a Reverse Proxy:
   ```nginx
   server {
     listen 80;
     location / {
       proxy_pass http://host.docker.internal:3001;
     }
   }
   ```
3. Visit `http://localhost`. Notice that Nginx forwards your request to Server A.

**Part 3: Implementing Load Balancing**
1. Update your Nginx configuration to include an `upstream` block:
   ```nginx
   upstream myapp {
     server host.docker.internal:3001;
     server host.docker.internal:3002;
   }
   
   server {
     listen 80;
     location / {
       proxy_pass http://myapp;
     }
   }
   ```
2. Refresh `http://localhost` multiple times. Observe how the response alternates between "Server A" and "Server B."

**Part 4: The Edge Security Gate**
1. Implement "Rate Limiting" in Nginx or your chosen Gateway.
2. Configure it to allow only 5 requests per minute from a single IP.
3. Rapidly refresh the page. After the 5th request, you should receive a `503 Service Unavailable` or `429 Too Many Requests`.
4. Discuss how this prevents "Denial of Service" (DoS) attacks on your application.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Session Stickiness. If a user logs into Server A, but the Load Balancer sends their next request to Server B, they will be "logged out" (unless you use a central session store like Redis). You can fix this with "Sticky Sessions" or "IP Hash" algorithms.
- **Gotcha 2:** SSL Termination. Usually, you decrypt HTTPS traffic at the Load Balancer (the Gateway) and send plain HTTP to your internal servers. This saves CPU resources on your application servers.

### Reflection Question
Why is an API Gateway essential for mobile applications that need to talk to 50+ different microservices? (Hint: Think about network bandwidth and battery life). drum
