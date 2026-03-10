# Exercise 001 - Authentication: Passwords & Beyond

### Objective
Identify the user. Master the basics of **Authentication** (Who are you?) vs **Authorization** (What can you do?). Learn how to move from "Plain Password" storage (Dangerous) to **Hashed & Salted** storage (Secure), and understand why modern systems are moving toward **Passwordless** and **Social Login**.

### Core Concepts to Master
- **Hashing:** A one-way function (like SHA-256) that turns a password into a scrambled string.
- **Salting:** Adding a random string (the "salt") to a password before hashing it to prevent "Rainbow Table" attacks.
- **Argon2 / BCrypt:** Specialized hashing algorithms designed to be "Slow" to prevent brute-force attacks.
- **The Login Session:** How the server "remembers" the user after the password check (Cookies vs Tokens).

### Research Topics
- "How to securely store passwords (OWASP guide)"
- "Hashing vs Encryption: The one-way rule"
- "What is a 'Salt' and why is it unique for every user?"
- "Argon2 vs BCrypt: Which is better?"

---

### The Practical Challenge

**Part 1: The "Hashed" Mistake**
1. You have a database of 1,000,000 users. 
2. Two users happen to pick the same password: `123456`.
3. If you only use a "Hash" (no salt), both users will have the SAME hash in your database.
4. Discuss: If a hacker finds ONE user's password is `123456`, how many other accounts can they break into instantly? (Answer: Everyone with that same hash).

**Part 2: The Salted Solution**
1. Research how **Salting** works: `Hash(salt + password)`.
2. Discuss why even if 1,000 users use the same password, the hashes in the database will be 1,000 DIFFERENT strings.

**Part 3: The "Wait" Penalty**
1. Research why **Argon2** is designed to take 0.5 seconds to calculate a hash on a fast server. 
2. Discuss: If a hacker can try 1,000,000,000 passwords per second with a regular hash (like MD5), how many can they try per second if each one takes 0.5 seconds? 
3. (Answer: Only 2 passwords per second!).

**Part 4: Identifying the method**
1. Research the **HIBP (Have I Been Pwned)** API. 
2. Discuss why it is a best practice to check a user's new password against "Leaked database" lists before letting them sign up.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Using MD5 or SHA-1. These are too fast and have "Collisions." Never use them for passwords.
- **Gotcha 2:** Password Complexity rules. Forcing a user to use "1 special character and 1 number" often results in weak passwords like `Password1!`. Encourage long "Passphrases" instead.

### Reflection Question
Why are companies like Google and Apple pushing for "Passkeys" (Biometrics) instead of "Passwords" in 2024? (Answer: To eliminate phishing and the risk of leaked databases).
