# Exercise 001 - API Styles: REST vs. GraphQL vs. gRPC

### Objective
Pick the language of the web. Master the three most common API architectures: **REST** (Resource-based), **GraphQL** (Query-based), and **gRPC** (Action-based). Learn which to use for your next Public API, your front-end mobile app, or your high-speed internal microservices.

### Core Concepts to Master
- **REST (Representational State Transfer):** Standard HTTP methods (`GET`, `POST`, `PUT`, `DELETE`). Results are always predictable. (Resource-based).
- **GraphQL:** The client asks for exactly the fields it needs. Solves the "Over-fetching" problem. (Query-based).
- **gRPC (Google Remote Procedure Call):** High-speed binary communication using **Protobuf**. Usually for backend-to-backend calls. (Procedure-based).
- **Over-fetching vs Under-fetching:** Getting too much data vs not enough.

### Research Topics
- "REST vs GraphQL vs gRPC: The ultimate guide"
- "When to use gRPC for microservices"
- "The power of GraphQL schemas"
- "Standardizing API responses (JSON:API specification)"

---

### The Practical Challenge

**Part 1: The "Over-fetching" Test (REST)**
1. You only need a user's `name`.
2. You call `GET /users/1`.
3. The server sends back 50 fields (`id`, `name`, `address`, `history`, `friends`, etc.).
4. Calculate the wasted bandwidth in MB if 1,000,000 users do this every day.

**Part 2: The GraphQL Solution**
1. You request: `user(id:1) { name }`.
2. The server sends back: `{"name": "Alex"}`.
3. Discuss: How does this help users on slow 3G mobile connections? (Answer: Reduces payload size significantly).

**Part 3: The gRPC Speed Test**
1. Research the difference between sending a JSON string (`'{"price": 10}'`) and a Protobuf binary (`\x0A`).
2. Discuss why gRPC is "Type-safe" (the compiler forces you to use the right fields) while REST is "String-based" (anyone can send a typo).

**Part 4: Identifying the style**
1. Which style for:
   - "A public API for thousands of unknown developers" (Answer: REST).
   - "A complex mobile app where users need to see data from 10 different tables on one screen" (Answer: GraphQL).
   - "Communication between the Order service and the Inventory service" (Answer: gRPC).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Caching. REST is easy to cache (every URL is a unique key). GraphQL is hard to cache because every query is a unique POST body.
- **Gotcha 2:** Security. In GraphQL, a malicious user can write a single query that "Joins" every table in your database, crashing the server. You need **Query Depth Limiting**.

### Reflection Question
Why has REST remained the most popular API style for 20 years despite newer "Better" technologies like GraphQL? (Answer: Simplicity, browser support, and universal caching).
