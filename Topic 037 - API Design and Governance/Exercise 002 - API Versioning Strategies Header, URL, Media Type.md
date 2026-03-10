# Exercise 002 - API Versioning Strategies

### Objective
Update without breaking. Master **API Versioning**—the art of releasing a "Version 2" of your API while still supporting the thousand legacy apps that use "Version 1." Compare the three primary techniques: **URL Versioning**, **Header Versioning**, and **Media Type Versioning**, and learn why "Changing a Response Field" is a breaking contract.

### Core Concepts to Master
- **URL Versioning:** `/api/v1/users` vs `/api/v2/users`. (The most common/easiest to see).
- **Header Versioning:** `X-API-Version: 2`. (Cleaner URLs, but harder to test in the browser).
- **Media Type Versioning:** `Accept: application/vnd.myapi.v2+json`. (The most "RESTful").
- **Breaking Change:** Deleting a field, changing a Type (Number to String), or renaming a field.
- **Graceful Deprecation:** Telling your users "V1 will be shut down in 6 months."

### Research Topics
- "API Versioning: URL vs Header vs Media Type"
- "Semantic Versioning (SemVer) for APIs"
- "Stripe's clever API versioning (Date-based)"
- "Using 'Sunset' and 'Deprecation' HTTP headers"

---

### The Practical Challenge

**Part 1: The Breaking Change Audit**
1. You have a response: `{"price": 10.99}`.
2. In Version 2, you change it to: `{"price": "10.99 USD"}`.
3. Discuss: If an old app does `price + 5`, what happens to the phone of the user? (Answer: The app crashes because it tried to add a Number to a String).

**Part 2: Comparison Battle**
1. **URL Versioning:** `GET /v1/products/1`.
   - Pro: Easy to bookmark, clear documentation.
   - Con: You must duplicate your code or use complex routing.
2. **Header Versioning:** `GET /products/1` + `X-API-Version: 2`.
   - Pro: "Clean" URLs.
   - Con: Harder to debug (you can't just share a link in Slack and have it "work" for someone else).

**Part 3: The Stripe Approach (Dates)**
1. Research how **Stripe** uses the `Stripe-Version: 2023-10-16` header.
2. Discuss why "Date-based" versioning is better for massive APIs that update once a week.

**Part 4: Identifying the strategy**
1. Research the **GitHub API**. Which versioning style do they use? 
2. Research the **Twitter (X) API**. Which do they use?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Supporting too many versions. If you have `v1`, `v2`, `v3`, and `v4` running simultaneously, you are paying 4x the price for servers and maintenance. Always have a "Deprecation" plan.
- **Gotcha 2:** The "Hidden" breaking change. Changing the order of an array is technically a breaking change for some poorly-written clients. Keep your responses stable!

### Reflection Question
Why are "Additive Changes" (adding a new field) usually not considered "Breaking," while "Subtractive Changes" (removing a field) are always breaking? (Answer: Because most clients just ignore fields they don't recognize).
