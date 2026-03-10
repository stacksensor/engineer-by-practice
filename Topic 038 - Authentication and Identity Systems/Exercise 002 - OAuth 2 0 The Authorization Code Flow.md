# Exercise 002 - OAuth 2.0: The Authorization Code Flow

### Objective
Delegate access. Master **OAuth 2.0**—the industry-standard protocol for authorization. Learn the **Authorization Code Flow**, designed for "Confidential" backend apps. Understand how to "Allow this website to read my Google Calendar" without giving the website your Google password.

### Core Concepts to Master
- **The Client:** The application asking for access (e.g., your website).
- **The Resource Owner:** The user who owns the data.
- **The Authorization Server:** The system that manages the "Login" (e.g., Google).
- **The Authorization Code:** A short-lived, one-time secret exchanged for a token.
- **The Access Token:** The "Passport" used to call the API.
- **Scopes:** The "Permissions" (e.g., `read_only`, `profile`, `calendar`).

### Research Topics
- "The 4 OAuth 2.0 Roles: Client, Owner, Server, Resource"
- "Authorization Code Flow: A visual step-by-step"
- "Redirect URIs: Why they must match EXACTLY"
- "State Parameter: Preventing CSRF attacks in OAuth"

---

### The Practical Challenge

**Part 1: The Redirect Dance**
1. You click "Login with Google."
2. Your browser is redirected to Google with a `client_id` and a `scope`.
3. You log in and click "Agree."
4. Google redirects you back to your own site with a `code=xyz-123`.
5. Discuss: Why does Google send a `code` instead of sending the `access_token` directly? 
6. (Answer: Security. The `code` is exchanged on the *backend* where no one can steal it!).

**Part 2: The Exchange (Backend)**
1. Your server sends the `code` + `client_secret` to Google's token endpoint.
2. Google gives your server an `access_token`.
3. Discuss: Is the `client_secret` safe on your server? (Yes). Is it safe in your JavaScript code? (No!).

**Part 3: The Scope Audit**
1. Research the scope list for the **GitHub API**. 
2. Discuss: If you only need to "Read a user's name," should you ask for the `repo` scope (full access to code)? 
3. (Answer: No, the **Principle of Least Privilege** says only ask for what you need).

**Part 4: Identifying the flow**
1. Which flow for:
   - "A Rails/Django server talking to Google" (Answer: Auth Code).
   - "A mobile app talking to Google" (Answer: PKCE - next exercise).
   - "A simple CLI tool talking to Google" (Answer: Device Flow).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Secret Leaks. Never commit your `client_secret` to Git! Use Environment Variables.
- **Gotcha 2:** Open Redirects. If you don't validate your `redirect_uri` against an "Allow List" in the Google console, a hacker can trick a user into sending their authorization code to the wrong website.

### Reflection Question
Why is OAuth 2.0 considered the single most important "Security" invention for the modern web? (Answer: It killed the practice of apps asking for your password directly).
