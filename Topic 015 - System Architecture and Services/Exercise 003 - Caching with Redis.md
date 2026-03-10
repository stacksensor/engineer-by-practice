# Exercise 003 - Caching with Redis

### Objective
Drastically reduce database load and response times. Implement Redis as an "In-Memory" cache layer to store frequently accessed data, allowing your application to serve requests in microseconds instead of milliseconds.

### Core Concepts to Master
- **In-Memory Store:** Redis is a key-value database that stores data in RAM, making it orders of magnitude faster than traditional Disk-based databases (SQL).
- **TTL (Time To Live):** Setting an expiration time on cached data (e.g., 60 seconds) after which the data is deleted to prevent "stale" information.
- **Cache-Aside Pattern:** Checking the cache first; if data is missing (a Cache Miss), fetch it from the database and write it to the cache for the next request.
- **Data Structures:** Using Redis beyond simple strings (Lists, Sets, and Hashes).

### Research Topics
- "What is Redis and why is it so fast?"
- "Cache-aside vs Write-through caching"
- "Common Redis use cases (Session management, rate limiting, results caching)"
- "Installing Redis with Docker"

---

### The Practical Challenge

**Part 1: The First Cache**
1. Launch Redis using Docker: `docker run -d --name my-redis -p 6379:6379 redis`.
2. Connect using a Node.js client (like `redis` or `ioredis`).
3. Implement a simple "Key-Value" test: Write "name: 'Alice'", then read it back. 
4. Observe the speed.

**Part 2: The Database Interceptor**
1. Create a "Slow" endpoint that simulates a heavy SQL query (use `setTimeout` for 2 seconds to simulate network lag).
2. Implement the "Cache-Aside" logic:
   ```javascript
   const cachedData = await redis.get(key);
   if (cachedData) return JSON.parse(cachedData);
   
   const freshData = await fetchFromDB(); // Slow
   await redis.set(key, JSON.stringify(freshData), 'EX', 60); // 60s TTL
   return freshData;
   ```
3. Call the endpoint once (it should be slow). Call it a second time (it should be nearly instant).

**Part 3: Stale Data & Invalidation**
1. Manually update a piece of data in your "Database" while it is still cached in Redis.
2. Note that the API still returns the old, "Stale" version from the cache. 
3. Implement "Immediate Invalidation": Update your `PUT` endpoint to call `redis.del(key)` whenever a record is updated.
4. Verify that the cache stays in sync with the database.

**Part 4: Session Management**
1. Redis is the industry standard for storing User Sessions.
2. Store a "Session Token" as a key in Redis, with a JSON object of user permissions as the value.
3. Set a long TTL (e.g., 24 hours). 
4. Discuss why storing sessions in RAM (Redis) is better for a distributed microservice cluster than storing them in a local server variable.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Cache Stampede. If a popular piece of data expires, 1000 users might hit the database simultaneously to refresh it. Solve this by pre-fetching data or using locking mechanisms.
- **Gotcha 2:** Serialization. Redis only stores strings or binary buffers. You must manually `JSON.stringify` objects going in and `JSON.parse` them coming out.

### Reflection Question
What are the negative consequences if your Redis cache is "too large" and fill up all the available RAM on the host machine? (Hint: Research 'Redis Eviction Policies'). drum
