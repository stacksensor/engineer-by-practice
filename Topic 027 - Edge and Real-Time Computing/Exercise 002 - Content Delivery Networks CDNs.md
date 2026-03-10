# Exercise 002 - Content Delivery Networks (CDNs)

### Objective
Scale the static and the dynamic. Master the operation of **Content Delivery Networks (CDNs)** like **Cloudflare**, **Fastly**, or **CloudFront**. Learn how to configure **Cache Headers** (`TTL`, `stale-while-revalidate`), and understand how "Edge Caching" reduces the load on your origin servers.

### Core Concepts to Master
- **Origin Server:** Your main database/server where the data starts.
- **Edge Cache:** The copy of your data stored on the CDN's global network.
- **Cache Hit vs. Cache Miss:** Whether the user's request was served by the CDN or had to go all the way back to your origin.
- **TTL (Time To Live):** How long an item stays in the cache before it's considered "stale."
- **Invalidation/Purging:** Explicitly telling the CDN to delete a cached item (e.g., when you update a product price).

### Research Topics
- "How do CDNs work? (Caching mechanisms)"
- "Cache-Control: public, max-age, stale-while-revalidate"
- "Understanding the CDN Cache Key"

---

### The Practical Challenge

**Part 1: The Header Lab**
1. Research the header `Cache-Control`.
2. Define a header that tells a CDN: "Cache this image for 1 year, but if it has been more than 24 hours since the last update, serve the old one while fetching the new one in the background." (Hint: `stale-while-revalidate`).

**Part 2: The Cache Key**
1. By default, the "Cache Key" is just the URL (e.g., `mysite.com/logo.png`).
2. Discuss what happens if you have different logos for mobile and desktop but they share the same URL. 
3. Research how "Vary" headers allow you to create multiple cache entries for the same URL.

**Part 3: Testing with Curl**
1. Use `curl -I https://www.github.com/` (or any site using a CDN).
2. Look for headers like `x-cache: HIT` or `cf-cache-status: HIT`.
3. If you see `MISS`, refresh the command. Does it turn into a `HIT`? Why?

**Part 4: Managing Dynamic Content**
1. Research "Edge Side Includes" (ESI) or "Server-side transformation at the edge."
2. Imagine a page with a static header (cacheable) and a personalized "Hello, User" name (non-cacheable).
3. How can a CDN merge these two to serve a fast, personalized page?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Caching Private Data. If you accidentally cache a `/user/profile` page with a public `TTL`, other users might see that user's private data! Rule #1: Never cache results from authenticated sessions unless you are extremely careful.
- **Gotcha 2:** The "Purge" delay. Purging (invalidating) a cache globally can take several seconds or even minutes. Don't rely on it for real-time updates (like a stock price).

### Reflection Question
How does a CDN help protect your origin server from a "Slashdot Effect" or a DDOS attack?
