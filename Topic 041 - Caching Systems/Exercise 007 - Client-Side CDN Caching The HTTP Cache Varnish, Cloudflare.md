# Exercise 007 - Client-Side & CDN Caching (HTTP Cache)

### Objective
Cache at the source. Master **HTTP Caching**—the art of using the user's browser (Client-side) and a **CDN** (Edge-side) to serve your data without the request ever touching your server. Learn which headers (`Cache-Control`, `ETag`, `Vary`) control this behavior and understand why caching a "Logo" is easy, but caching a "User Profile" is dangerous.

### Core Concepts to Master
- **Browser Cache (Client-side):** The browser saves an image on the user's local disk/RAM.
- **CDN (Content Delivery Network):** A server in the user's city (e.g., Tokyo, London, NYC) saves a copy for every user in that city. (Tools: Cloudflare, Akamai, CloudFront).
- **Cache-Control Header:** `max-age=3600`. Telling the browser "Don't ask me for this file again for 1 hour."
- **ETag (Entity Tag):** A unique "Hash" of a file (e.g., `xyz-123`). If the ETag hasn't changed, the server returns `304 Not Modified` (Very fast!).
- **Purge / Flush:** Telling the CDN to "Delete everything! I have a new version!"
- **Public vs Private Cache:** Allowing a CDN to cache it vs Only allowing the user's browser.

### Research Topics
- "How HTTP Cache-Control headers work"
- "Browser Cache vs Edge/CDN Cache: A comparison"
- "The ETag (Entity Tag) and '304 Not Modified' flow"
- "What is a 'Vary' header and why is it for Gzip vs Brotli?"

---

### The Practical Challenge

**Part 1: The "Logo" Test (Conceptual)**
1. You have a 1MB Logo. 1,000,000 users visit your site in 1 hour.
2. **No Cache:** You send 1,000,000 MB (1TB) of data over the internet ($$$). 
3. **With Browser Cache:** 1,000,000 users download it ONCE. Total data: 1MB.
4. Discuss: Is your server "Faster," or did you just "Save" money? (Answer: Both!).

**Part 2: The ETag Dance in DevTools**
1. Open Chrome DevTools -> Network. 
2. Refresh a major site twice. 
3. Observe the "Status" column. Find a **`304 Not Modified`**.
4. Look at the **`ETag`** header in the response. 
5. Discuss: Did the browser actually download any bytes for that file during the 2nd refresh? (Answer: No, only the small header).

**Part 3: The "Private" Disaster**
1. You have a page `GET /my-account`. It shows the User's name.
2. You set `Cache-Control: public, max-age=3600`.
3. User A visits the page. The CDN caches it.
4. User B (on the same Wi-Fi) visits the page.
5. Discuss: Does User B see User A's name? 
6. (Answer: Yes! **Public** means any proxy can cache it. Use **`private`** for personal data!).

**Part 4: Identifying the strategy**
1. Research the **Cloudflare** Cache Everything vs Standard settings. 
2. Discuss why caching a "JSON API" is much harder than caching a "CSS file." (Answer: JSON data changes frequently; CSS changes only when you deploy).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Immoral" Cache. If you set `max-age=1 year`, and you change the file, you cannot "force" the user's browser to update until 1 year has passed! (Solution: Use "Cache Busting" - name your files `style.v123.css` instead of `style.css`).
- **Gotcha 2:** The "Cookie" problem. If your CDN caches a page that contains a "Cart" or "Login" status, it might show that status to everyone on the internet.

### Reflection Question
Why is the "Edge Cache" (CDN) considered the most effective way to improve the speed of an app for "Global" users? (Answer: Because moving data from NYC to London is limited by the Speed of Light, but moving data from a London Data center to a London house is instant).
