# Exercise 002 - Secure Data: Encryption at Rest and in Transit

### Objective
Shield the bits. Learn how to protect sensitive user data (PII) by using **AES-256** and **TLS 1.3**. Understand why a "Stolen Hard Drive" should be worthless to a criminal because the data is unreadable.

### Core Concepts to Master
- **Encryption at Rest:** Data on the SSD is encrypted (e.g., AWS EBS encryption).
- **Encryption in Transit:** Data on the Wire is encrypted (e.g., HTTPS/TLS).
- **AES-256 (Symmetric):** The "Gold Standard" for fast, private encryption.
- **Envelope Encryption:** Using a **Master Key (KMS)** to encrypt your "Data Key" which encrypts the data.
- **Salt and Hashing:** Why you NEVER store a "Cleartext" password.

### Research Topics
- "TLS 1.3: Improvements and why you should migrate"
- "AWS KMS: How to encrypt an S3 bucket with 1-click"
- "Salting passwords in Node.js with Argon2 or Bcrypt"
- "Full Disk Encryption (FDE) vs. Database Row Encryption"

---

### The Practical Challenge

**Part 1: The "Loud" Network (Scenario)**
1. You are in a coffee shop. You log in to a "Bank" via **HTTP** (unencrypted).
2. A hacker is sitting next to you.
3. **The Disaster:** They see your "Password: 123" in their screen. 
4. **The fix:** 
   - Research **TLS 1.3 (HTTPS)**. 
   - Discuss: How does the "Public Key" handshake make it impossible for the hacker to read the password?
   - Answer: Because only your computer and the Bank's computer have the "Secret Key."

**Part 2: The "Stolen" Disk (Math)**
1. Your company database is stolen.
2. In it, you have 1,000,000 Credit Card numbers. 
3. **If Unencrypted:** The company is dead. Fined billions.
4. **If Encrypted (AES-256):** 
   - Research the "Time to Crack" AES-256. 
   - Discuss: If it takes 1,000 trillion years, is the data actually "Safe"?
   - Answer: Yes. **The data is worthless without the Key.**

**Part 3: The "Argon2" Password (Concept)**
1. Research **Argon2** or **Bcrypt**. 
2. Discuss why "Hashing" is one-way (you can't decrypt it) while "Encryption" is two-way.
3. Answer: Because you don't *need* to know the password; you only need to know if the *Hash* matches.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Hardcoded" Keys. Putting your encryption key in `config.js` or `Main.java`. (Solution: Use a **Secrets Manager** (AWS, HashiCorp Vault)).
- **Gotcha 2:** Legacy TLS. Using **TLS 1.0 or 1.1**. (Answer: These are "Broken" and can be cracked in minutes).

### Reflection Question
Why is "Data in Transit" (the wire) usually harder to secure than "Data at Rest" (the disk)? (Answer: Because you control the disk, but you don't control the 20 routers and cables between your computer and the server).
