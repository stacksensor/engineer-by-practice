# Exercise 005 - JWT (JSON Web Tokens) Deep Dive

### Objective
Trust the token. Master **JWT (JSON Web Tokens)**—the standard for "Stateless" authentication. Learn the anatomy of a JWT (**Header**, **Payload**, **Signature**), the difference between **Symmetric** (HMAC) and **Asynchronous** (RSA/ECDSA) signing, and how to protect your app from the common "None Algorithm" attack.

### Core Concepts to Master
- **The Header:** Specifies the algorithm (e.g., `HS256`, `RS256`).
- **The Payload:** The claims (e.g., `sub`, `name`, `admin: true`).
- **The Signature:** The piece that proves the token hasn't been tampered with.
- **Symmetric Signing (HS256):** One "Secret" key to both Sign and Verify. (Fast but harder to share).
- **Asymmetric Signing (RS256):** A "Private" key for the issuer (to sign) and a "Public" key for everyone else (to verify). (Safer for large systems).
- **Base64URL:** The encoding (NOT encryption) used for the 3 parts of the JWT.

### Research Topics
- "How to read a JWT manually (using jwt.io)"
- "HS256 vs RS256: Which to choose when?"
- "Common JWT security vulnerabilities: The 'alg: none' attack"
- "Storing JWTs in the browser: Cookies vs LocalStorage"

---

### The Practical Challenge

**Part 1: The "Encryption" Myth**
1. Copy an example JWT from a tutorial into **jwt.io**. 
2. Observe how the "Payload" is instantly readable without any secret key.
3. Discuss: Why should you NEVER put a user's password, SSN, or private phone number inside a JWT?
4. (Answer: Anyone can decode a JWT; they just can't *change* it).

**Part 2: The Tamper Test**
1. Take a valid JWT that says `role: user`.
2. Delete the "Signature" (the 3rd part).
3. Change the payload to say `role: admin`.
4. Discuss why the server will REJECT this token (Answer: The signature no longer "Matches" the new admin payload).

**Part 3: The "alg: none" Attack**
1. Research how early JWT libraries had a bug where they would trust a token if the header said: `{ "alg": "none" }`.
2. Discuss why this allowed anyone to become a "Super Admin" just by editing the JSON.
3. How do modern libraries fix this? (Answer: You MUST specify the algorithm you expect in your code).

**Part 4: Identifying the storage**
1. Research the pros and cons of:
   - **LocalStorage:** (Easy to use but vulnerable to XSS). 
   - **HttpOnly Cookies:** (More secure but can be hard to set up with CORS).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Secret too short. If you use a weak secret like `password` for HS256, a hacker can "Brute force" the signature and recreate their own tokens. Use a 256-bit random key.
- **Gotcha 2:** Missing `exp` claim. If you don't include an "Expiration Time" (`exp`), a token is valid forever. If a laptop is stolen, the token will work for the rest of eternity.

### Reflection Question
Why are JWTs better for "Scale" than traditional "Session IDs" that require a database check on every request? (Answer: Because the server only needs to do local "Math" (Signature check) to trust the user).
