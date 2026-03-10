# Exercise 006 - Rate Limiting & Circuit Breakers

### Objective
Protect your services from being overwhelmed. Master **Rate Limiting** to control incoming traffic (defending against DDOS and hungry scripts) and **Circuit Breakers** to handle outgoing traffic (protecting your own service from waiting on a slow/dead external API).

### Core Concepts to Master
- **Rate Limiting:**
  - **Fixed Window:** X requests per minute.
  - **Token Bucket:** Allows for "bursty" traffic while maintaining a long-term average.
  - **Leaky Bucket:** Force a constant rate of traffic.
- **Circuit Breaker:** A pattern that monitors failures.
  - **Closed:** Everything is normal. Requests flow.
  - **Open:** Too many failures detected. Requests are blocked immediately (fail-fast) without even trying to call the external service.
  - **Half-Open:** Periodically test if the external service is healthy again.

### Research Topics
- "Rate limiting algorithms for developers"
- "The Circuit Breaker pattern explained"
- "Using Redis for distributed rate limiting"

---

### The Practical Challenge

**Part 1: The Token Bucket**
1. Research the **Token Bucket** algorithm.
2. Imagine your API allows 5 requests per second, with a "Burst" capacity of 10.
3. If a bot sends 12 requests in 500ms, how many will succeed? If a human sends 1 request every 200ms, will they ever be throttled?

**Part 2: Distributed Rate Limiter (Logic)**
1. Design a simple rate limiter using Redis `INCR` and `EXPIRE`.
2. Flow: `Key = user_id:minute`. Every request increments the key. If value > Limit, return 429 (Too Many Requests). 
3. Discuss why this "Fixed Window" approach might be unfair at the boundary of a minute (e.g., getting 100 requests at 11:59:59 and 100 at 12:00:00).

**Part 3: The Circuit Breaker (Simulation)**
1. Write a Python or Node.js script that calls a "Dummy" API that fails 100% of the time.
2. Use a library like `pycircuitbreaker` or `opossum`. 
3. Configure it to "Open" the circuit after 5 consecutive failures.
4. Observe that after the 6th call, your code returns a "Circuit Open" error instantly, without even attempting the network request. This saves your resources (memory/threads).

**Part 4: Fallbacks**
1. When the circuit is **Open**, what should you return to the user?
2. Design a "Fallback" (e.g., if the "Personalized Recommendations" service is down, the Circuit Breaker returns a generic "Trending Products" list stored in local cache).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Global vs Local Rate Limiting. If you run 10 instances of your API, and each has a "Local" limit of 10 requests, a user could send 100 requests total. You need a "Global" store like Redis if you want a true "10 per user" limit.
- **Gotcha 2:** The "Thundering Herd." When a Circuit Breaker moves from Open to Half-Open and finally to Closed, 10,000 waiting requests might all flood the external service at once, instantly crashing it again. Use "Jitter" or slow ramp-ups.

### Reflection Question
How does a Circuit Breaker prevent a "Cascading Failure" (where one slow microservice causes every other service in the company to also slow down and crash)?
