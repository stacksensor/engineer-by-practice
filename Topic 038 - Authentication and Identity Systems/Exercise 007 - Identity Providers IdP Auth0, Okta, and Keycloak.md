# Exercise 007 - Identity Providers (IdP): The Choice

### Objective
Infrastructure for users. Master the various tools for managing user accounts. Compare **Managed IdPs** (SaaS) like **Auth0**, **Okta**, and **Clerk** vs **Self-Hosted IdPs** (Open Source) like **Keycloak** or **Supabase Auth**. Learn why "Building your own Auth" is the most common mistake for a new developer.

### Core Concepts to Master
- **The IdP (Identity Provider):** A specialized service that handles Login, Sign-up, Password resets, and Social connections.
- **SaaS IdP:** High cost, zero maintenance, extremely secure. (Auth0, Okta, Firebase).
- **Self-Hosted IdP:** Zero cost (licensing), high maintenance, requires server management. (Keycloak, Authentik).
- **Embedded vs Redirect:** Showing a "Login" box inside your React app vs sending a user to a separate "Hosted" login page.
- **Multi-tenancy:** Allowing "Company A" to have its own set of 100 users, and "Company B" to have another set. (Critical for B2B apps).

### Research Topics
- "Auth0 vs Keycloak: A head-to-head comparison"
- "Why you should never build your own authentication"
- "Supabase Auth and the 'GoTrue' engine"
- "The concept of 'Branded' login pages"

---

### The Practical Challenge

**Part 1: The "Don't Build Your Own" Test**
1. List 5 things a "Simple" sign-up form actually needs to handle in order to be professional:
   - (Answer: 1. Password hashing/salting, 2. Email verification, 3. Password reset flow, 4. MFA setup, 5. Detection of 'Leaked' passwords, 6. Bot detection/Captcha).
2. Discuss why writing all 6 correctly would take a 2-person team 3 months of work.

**Part 2: The SaaS Logic (Auth0/Clerk)**
1. Research the "Free Tier" of **Clerk** or **Auth0**. 
2. Discuss why a startup with 10 users should pick a SaaS IdP even if it eventually becomes expensive. 
3. (Answer: Speed to market and zero security risk).

**Part 3: The Self-Hosted Logic (Keycloak)**
1. Research **Keycloak**. 
2. Discuss: If a company has 10,000,000 users, why would they switch from Auth0 ($$$ per user) to a self-hosted Keycloak (flat server cost)?

**Part 4: Identifying the IdP**
1. Which IdP for:
   - "A Next.js side project I want to finish in 2 days" (Answer: Clerk / NextAuth).
   - "A massive bank with strict data residency laws that says 'No data in the US Cloud'" (Answer: Keycloak on-premise).
   - "A B2B SaaS app that needs to allow customers to 'Login with their own company SSO'" (Answer: Auth0 / WorkOS).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Vendor Lock-in. If you move 1,000,000 users to a SaaS IdP, it can be very hard to move them "out" if the price increases, because the SaaS provider might not give you the raw password hashes.
- **Gotcha 2:** The "Shadow" Auth. Some developers use a library (like `next-auth`) but don't realize it's still "Hand-building" the security rules on their own server.

### Reflection Question
Why is "Authentication" often called the "Front Door" of a business, both for the user's experience and for its largest security risk? (Answer: It’s the first thing every user sees, and the first thing every hacker tries to break).
