# Exercise 004 - Rate Limiting & Quotas (Throttling)

### Objective
Protect the server. Master **Rate Limiting**—the technique of deciding how many requests a user (or an IP, or an API Key) can make in a set period. Learn about the **Token Bucket** and **Leaky Bucket** algorithms, and understand how to communicate limits to users via **HTTP 429** and **Headers (X-RateLimit)**.

### Core Concepts to Master
- **Rate Limit:** e.g., "100 requests per minute."
- **Quotas:** e.g., "10,000 requests per month."
- **Token Bucket Algorithm:** A conceptual bucket of 100 "tokens" that refills 1 token per second. Every request takes 1 token. When empty, requests are blocked.
- **Fixed Window vs. Sliding Window:** Counting 100 requests from 12:00-12:01 vs counting 100 requests in any 60-second span.
- **HTTP 429 (Too Many Requests):** The standard status code for rate limiting.

### Research Topics
- "How to implement rate limiting with Redis"
- "Token Bucket vs Leaky Bucket algorithm"
- "Fixed Window vs Sliding Window Log rate limiting"
- "Reading X-RateLimit-Remaining and X-RateLimit-Reset headers"

---

### The Practical Challenge

**Part 1: The Token Bucket Math**
1. Bucket Capacity: 100. Refill Rate: 10/min.
2. A user makes 100 requests at 12:00:00. 
3. They have 0 tokens left.
4. When can they make their next 10 requests? (Answer: 1 minute later, at 12:01:00).
5. Discuss: Why does this allow "Burstiness" (e.g., loading 10 images at once) while preventing long-term abuse?

**Part 2: Fixed Window Flaw**
1. Your limit is 100 per minute.
2. User makes 100 requests at `12:00:59`.
3. User makes 100 requests at `12:01:01`.
4. Discuss: How did they just make 200 requests in 2 seconds without being blocked? (Answer: The "Edge of the minute" reset).
5. How does a **Sliding Window** fix this?

**Part 3: The Communicative Response**
1. Research the headers:
   - `X-RateLimit-Limit`: (Answer: 100).
   - `X-RateLimit-Remaining`: (Answer: 45).
   - `Retry-After`: (Answer: 30 seconds).
2. Discuss why these are the "Friendly" way to tell a developer "Slow down!"

**Part 4: Identifying the level**
1. Where should you rate limit?
   - **IP-based:** (Best for: Preventing DDoS from one machine).
   - **User/Key-based:** (Best for: Monetizing your API - lower limit for free users).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Race conditions. If two requests from the same user hit two different servers at once, they might both check Redis, see "1 token left," and both succeed—resulting in 101 requests! Use **Redis Lua Scripts** to prevent this.
- **Gotcha 2:** The "Shared IP" problem. If you rate-limit by IP, you might accidentally block 10,000 students at a university because they all share one "Public IP."

### Reflection Question
Why is Rate Limiting essential for the "Stability" of your database, even if you trust your users? (Answer: To prevent a bug in the user's code from turning into an unintended DDoS attack on your server).
