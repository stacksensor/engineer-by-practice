# Exercise 006 - MFA & WebAuthn (Passwordless)

### Objective
Beyond the password. Master **Multi-Factor Authentication (MFA)** and the new standard for browser security: **WebAuthn**. Learn how to combine "Something you know" (Password) with "Something you have" (Authenticator App/YubiKey) or "Something you are" (Biometrics/FaceID). Understand why **Passkeys** are the future of the internet.

### Core Concepts to Master
- **2FA / MFA:** Adding a second step to the login process.
- **SMS MFA (Insecure):** Sending a code via text. Highly vulnerable to "SIM Swapping."
- **TOTP (Authenticator Apps):** A standard algorithm (Time-based One-Time Password) used by Google Authenticator, Authy, etc.
- **WebAuthn (Passkeys):** A W3C standard that allows the browser to use hardware keys (USB) or built-in biometrics (TouchID/Windows Hello) to log in without a password.
- **Public Key Cryptography:** How WebAuthn uses a "Private Key" on your phone and a "Public Key" on the server.

### Research Topics
- "Why SMS 2FA is no longer enough"
- "How TOTP (Time-based One-Time Password) works (The math)"
- "What is a 'Passkey' and how do I use it? (passkeys.io)"
- "Implementing MFA in a custom app (The 'QR Code' step)"

---

### The Practical Challenge

**Part 1: The TOTP Math (Conceptual)**
1. You have a "Secret Key": `ABCD-1234`.
2. The server and your phone both know this key.
3. Every 30 seconds, they both do: `Hash(Secret Key + The Current Time)`.
4. Result: `123 456`.
5. Discuss: Why does this code work even if your phone has NO internet connection? (Answer: Because the "Time" is the only thing that changes!).

**Part 2: The Passkey Experience**
1. Visit: `https://webauthn.io` (a playground for testing WebAuthn).
2. Click "Register" and use your TouchID or FaceID. 
3. Observe how the server stores a **Public Key** but NOT your fingerprint.
4. Discuss: If the website's database is hacked, can the hacker "Steal" your fingerprint? 
5. (Answer: No, the server only has the math key, not the biologics).

**Part 3: Recovery Codes**
1. Discuss: If a user loses their phone (TOTP) and their Security Key (WebAuthn), how do they get into their account?
2. Research the concept of **"Recovery Codes"** (one-time use strings to print and put in a safe).

**Part 4: Identifying the "Factor"**
1. Which factor for:
   - "Fingerprint" (Answer: Something you are).
   - "A physical YubiKey" (Answer: Something you have).
   - "A birth date" (Answer: Something you know).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** SMS Hijacking. Hackers can call a phone company, pretend to be you, and "Move" your phone number to their own SIM card. They can then steal your 2FA codes. Avoid SMS whenever possible.
- **Gotcha 2:** Implementing MFA too late. Once a user's account is already compromised, it is often too late to "Add" MFA because the hacker will have already added THEIR OWN phone number.

### Reflection Question
Why are "Push Notifications" (like on a Google or Apple account) considered more secure and user-friendly than "Typing a 6-digit code"? (Answer: Faster, clearly shows the "Location" of the login, and harder to "Phish" into a fake website).
