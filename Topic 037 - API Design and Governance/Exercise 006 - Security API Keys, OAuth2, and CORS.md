# Exercise 006 - Security: API Keys, OAuth2, and CORS

### Objective
Lock the door. Master the three most common ways to secure an API: **API Keys** (Simple, server-to-server), **OAuth2/JWT** (Complex, user-to-server), and **CORS** (Browser-to-server). Learn when to use a simple "Secret String" and when to use a full "Token-based" system.

### Core Concepts to Master
- **API Key:** A long, secret string (e.g., `sk_live_123`). Usually for server-side talk or simple tools. Avoid sending these from a browser!
- **OAuth 2.0:** The "Standard" for delegating access (e.g., "Allow this app to read my Google Calendar").
- **JWT (JSON Web Token):** A stateless, signed token containing user info (e.g., `role: admin`). The server doesn't need to check its database for every request.
- **CORS (Cross-Origin Resource Sharing):** The browser's way of asking "Am I allowed to talk to `api.google.com` from `mywebsite.com`?"

### Research Topics
- "API Keys vs OAuth 2.0: When to use which"
- "How JWT (JSON Web Tokens) work: Header, Payload, Signature"
- "The OAuth 2.0 Authorization Code Flow"
- "Understanding CORS errors and 'Preflight' requests"

---

### The Practical Challenge

**Part 1: The "API Key" Mistake**
1. You put your `STRIPE_API_KEY` in your React/Frontend code.
2. A hacker right-clicks "View Source" and finds it.
3. Discuss: What can the hacker do to your bank account? 
4. How do you fix this? (Answer: Never send keys from frontend; only from backend).

**Part 2: The Stateless JWT (Concept)**
1. User logs in. Server gives them a **JWT**. 
2. The JWT says: `{ "user": "Alex", "exp": "2024-10-10", "role": "admin" }`.
3. The server signs it. 
4. Alex sends this on every request: `Authorization: Bearer <jwt>`.
5. Discuss: If the server is offline from the database, can it still "Trust" that Alex is an admin? (Answer: Yes, by verifying the signature).

**Part 3: The CORS Preflight**
1. Research the **OPTIONS** request. 
2. Discuss why the browser sends this "Empty" request *before* sending your actual POST request. 
3. What is the response header that allows your website to talk to the API? (Answer: `Access-Control-Allow-Origin`).

**Part 4: Identifying the auth**
1. Which security for:
   - "A CLI tool that uploads logs to a server" (Answer: API Key).
   - "A mobile app where a user logs in with their Google account" (Answer: OAuth2).
   - "An internal service talking to the database" (Answer: mTLS / Hardcoded Key).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** JWT Expiration. If your tokens never expire, a stolen token is a lifetime pass for a hacker. Use short-lived (15m) access tokens and long-lived refresh tokens.
- **Gotcha 2:** CORS * isn't always safe. Setting `Allow-Origin: *` allows EVERY website on the internet to talk to your API. Only do this if your API is public and has no private data.

### Reflection Question
Why are "Scoped" API keys (e.g., 'Read-only' vs 'Full Access') the best practice for professional APIs? (Answer: Principle of Least Privilege - if a key is stolen, the damage is limited).
