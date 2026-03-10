# Exercise 007 - API Performance: Caching & Pagination

### Objective
Scale the result. Master the performance essentials for APIs. Learn how to handle "Massive Data" by using **Pagination** (Dividing results into pages), specifically the **Cursor-based** approach (used by Facebook and Slack) vs the **Offset-based** approach. Understand **Cache-Control** and how to use a "CDN" to serve your API results in milliseconds.

### Core Concepts to Master
- **Offset-based Pagination:** `page=5&limit=20`. (Easy but slow for large tables; has "Skipping" bugs).
- **Cursor-based Pagination:** `after=UUID_123&limit=20`. (Extremely fast; consistent even if new data is added synchronously).
- **Cache-Control Header:** `max-age=3600`. Telling the user's browser (or a CDN) "Don't ask me for this data again for 1 hour."
- **ETag:** A unique "Hash" of the response. If the data hasn't changed, the server says `HTTP 304 (Not Modified)`, saving bandwidth.
- **Conditional GET:** Using the `If-None-Match` header.

### Research Topics
- "Offset vs Cursor-based pagination: Performance comparison"
- "How to implement cursor-based pagination in Postgres"
- "Stripe's API Caching strategy"
- "Understanding Cache-Control: max-age, stale-while-revalidate, and public/private"

---

### The Practical Challenge

**Part 1: The "Skip" Problem (Offset)**
1. You show "Page 1" (Users 1-10).
2. While the user is reading, someone inserts a NEW user at the top (User 0).
3. The user clicks "Page 2" (`offset=10`).
4. Result: User 10 (who was at the bottom of Page 1) is now at the top of Page 2. 
5. The user sees the same person twice!
6. Discuss: How does a **Cursor** (pointing to the ID of the last user seen) fix this?

**Part 2: The Offset Penalty (Math)**
1. Research why `OFFSET 1000000` is slow in SQL. 
2. (Answer: The database has to "Count" 1 million rows and throw them away before giving you the 1,000,001st row). 
3. Discuss why a Cursor (`WHERE id > 1000000`) is instant (Index Seek).

**Part 3: The Cache Header**
1. Research the header: `Cache-Control: public, max-age=3600`.
2. Discuss why a "Price API" should NOT use this, but a "List of Countries API" should.

**Part 4: Identifying the strategy**
1. Research the **Facebook Graph API**. 
2. Research the **Slack Web API**. 
3. Which pagination style do they both use? (Answer: Cursor-based).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Cursors and Sorting. Cursors are easy for "ID" sort, but very hard for "Score" or "Alphabetical" sort if the values change frequently.
- **Gotcha 2:** Stale Cache. If you cache `user_profile` for 1 hour, and the user changes their name, they will be very confused when they refresh the page and see their OLD name! Use **Cache Invalidation** or "Low TTL" for profile data.

### Reflection Question
Why is "Pagination" and "Caching" the most important part of keeping an API "Free" or "Cheap" to run for a company? (Answer: Because it reduces the number of expensive database queries).
