# Exercise 007 - Design for Failure (Bulkheads & Timeouts)

### Objective
Embrace the "Chaos." Stop trying to build "Perfect" systems and start building "Antifragile" systems that expect components to fail. Master **Bulkheading** to isolate failures, and implement aggressive **Timeouts** and **Retries with Jitter** to ensure the cluster remains stable under pressure.

### Core Concepts to Master
- **The Bulkhead Pattern:** Partitioning resources (e.g., Thread Pools or Database connections) so that if one feature hangs, it doesn't consume all the resources of the entire application.
- **Fail-Fast & Timeouts:** Never wait forever. Every network call should have a timeout (e.g., 2 seconds).
- **Retries with Exponential Backoff:** Waiting longer and longer between retries (`2ms`, `4ms`, `8ms`, ...) to avoid overwhelming a struggling service.
- **Jitter:** Adding a random amount of time to your retries so that 1000 failing clients don't all retry at the exact same millisecond.
- **Graceful Degradation:** The ability of a system to continue operating (at a reduced level) when some parts are broken.

### Research Topics
- "Architecting for failure: Bulkheads and Timeouts"
- "The importance of Jitter in distributed systems"
- "How Netflix uses chaos engineering"

---

### The Practical Challenge

**Part 1: The Bulkhead Simulation**
1. Imagine an API with two endpoints: `GET /search` and `GET /billing`. Both share a single "Thread Pool" of 10 workers.
2. If `/billing` starts taking 60 seconds because of a slow database, explain how a user trying to run a simple `/search` will be blocked.
3. Redesign the system to use "Bulkheads" (e.g., 7 workers for Search, 3 workers for Billing). Observe how the Search endpoint stays fast even when Billing is totally frozen.

**Part 2: The Timeout Test**
1. Write a script that calls a server that takes exactly 10 seconds to respond.
2. Set a client-side timeout of 2 seconds.
3. Observe the `TimeoutError`. Discuss why your server resource (a thread) is freed up 8 seconds earlier than it would have been otherwise.

**Part 3: Retries & Jitter (Code)**
1. Write a loop that retries a failing function 5 times.
2. Implement **Exponential Backoff**: `wait = 2^retry_number * 100ms`.
3. Add **Jitter**: `wait = wait + random(0, 50ms)`.
4. Run 100 instances of this script and plot the "Wait Times." Observe how the load is spread out across time instead of arriving in "Waves."

**Part 4: Graceful Degradation (Conceptual)**
1. Design a "News Site" architecture.
2. Component A: Current News (Critical).
3. Component B: Weather Widget (Non-critical).
4. Component C: "Recommended for You" AI (Non-critical).
5. Explain how the site should look if Components B and C are down. (e.g., The site hides those widgets but the News still loads).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Retry Storm." If 1 million devices are disconnected from a server and they all retry every 1 second, they will DDOS the server the moment it tries to come back online. Jitter is the only cure.
- **Gotcha 2:** Wrong Timeout Values. If your timeout is too short (e.g., 10ms for a global database query), you will constantly fail even when the system is healthy. Always base timeouts on the `99th percentile` (p99) latency of the service.

### Reflection Question
Why is "Failing Fast" (returning an error quickly) often better for the overall health of a system than "Trying Hard" (waiting and retrying forever)?
