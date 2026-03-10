# Exercise 004 - OpenID Connect (OIDC): Identity on top of OAuth

### Objective
Meet the user behind the token. Master **OpenID Connect (OIDC)**—the identity layer that sits on top of OAuth 2.0. Learn how the **ID Token** (a JWT) allows your app to know the user's name, email, and profile picture, and how it differs from the **Access Token** (used to call APIs).

### Core Concepts to Master
- **The ID Token:** A JWT containing "Identity" information about the user.
- **The UserInfo Endpoint:** A standard URL where you can ask for more profile details.
- **Claims:** The specific "facts" about a user (e.g., `given_name`, `email_verified: true`).
- **Discovery Document:** A `.well-known/openid-configuration` JSON file that tells your app "Here are the Google OIDC URLs."
- **Standard Scopes:** `openid`, `profile`, `email`, `address`, `phone`.

### Research Topics
- "OpenID Connect vs OAuth 2.0: The key difference"
- "Reading the Google OIDC Discovery Document"
- "What is an 'ID Token' and how do I verify it?"
- "The importance of the 'openid' scope"

---

### The Practical Challenge

**Part 1: The Access vs Identity Test**
1. You have a key to a hotel room.
   - **OAuth (Access Token):** The key lets you into the room (Access). 
   - **OIDC (ID Token):** The key has your name on it and proves you are the one who booked it (Identity).
2. Discuss: Why does a "Login with Google" button need OIDC but a "Read my Calendar" script only needs OAuth?

**Part 2: The ID Token JSON**
1. An ID Token looks like this:
   - `{ "iss": "google.com", "sub": "123-user-id", "email": "alex@gmail.com", "exp": 17263544 }`.
2. Research the `sub` (Subject) field. 
3. Discuss: Why should you always store the `sub` ID in your database instead of the `email`? 
4. (Answer: Emails can change; the `sub` ID is unique and permanent forever).

**Part 3: The Well-Known Discovery**
1. Visit: `https://accounts.google.com/.well-known/openid-configuration`.
2. Find:
   - `issuer`: (The ID of the server).
   - `authorization_endpoint`: (Where users log in).
   - `jwks_uri`: (Where the "Public Keys" for verifying tokens live).
3. Discuss why this one file makes OIDC "Self-documenting" for any app.

**Part 4: Identifying the claim**
1. Research the **GitHub OIDC** implementation. 
2. Does it provide a `email_verified` claim? (Answer: Yes, and it’s critical for security!).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Trusting the data without verification. Never extract the `email` from an ID Token until you have verified the "Signature" using the public keys from the `jwks_uri`.
- **Gotcha 2:** The `nonce` parameter. When doing OIDC, you should send a random `nonce` string. If the ID Token doesn't contain that EXACT same string, someone is trying to replay an old token on you!

### Reflection Question
Why is OIDC the reason that "Login with Apple" and "Login with Microsoft" look and act 100% identical for developers? (Answer: Standardized protocols and Discovery documents).
