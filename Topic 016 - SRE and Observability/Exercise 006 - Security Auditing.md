# Exercise 006 - Security Auditing & Pen Testing

### Objective
Think like a hacker to protect your users. Learn to identify and mitigate the world's most common security vulnerabilities (the OWASP Top 10), and use automated tools to "Penetrate" your own application to find holes before malicious actors do.

### Core Concepts to Master
- **OWASP Top 10:** The industry-standard list of the most critical web application security risks (SQLi, XSS, Broken Auth, etc.).
- **SQL Injection (SQLi):** Attacking a database by injecting malicious SQL code into input fields (Solved by using Prepared Statements/ORMs).
- **Cross-Site Scripting (XSS):** Injecting malicious scripts into web pages viewed by other users.
- **CSRF (Cross-Site Request Forgery):** Tricking a user's browser into performing an action they didn't intend to.
- **Vulnerability Scanning:** Using tools like **OWASP ZAP** or **npm audit** to find outdated libraries with known exploits.

### Research Topics
- "What is the OWASP Top 10 2024?"
- "Preventing SQL injection in Node.js"
- "How to handle XSS in React apps"
- "Security headers (CSP, HSTS) explained"

---

### The Practical Challenge

**Part 1: The Vulnerable Input**
1. Create a simple "Login" form that uses a raw SQL string: 
   `const query = "SELECT * FROM users WHERE email = '" + req.body.email + "';"`
2. Log in as a hacker without knowing the email or password.
3. Input: `' OR 1=1; --`.
4. Observe how the database returns the first user (likely the admin) because the query becomes `SELECT * FROM users WHERE email = '' OR 1=1;`. 
5. Fix the code by using **Prepared Statements** (`?` placeholders).

**Part 2: The Stored XSS Attack**
1. Build a "Comment" system that saves users' comments and displays them on a page.
2. As a "User", post a comment containing a script: `<script>alert('Hacked!');</script>`.
3. Refresh the page. If the alert appears, your site is vulnerable to XSS.
4. If you use React, note that it automatically sanitizes data by default using `{}`. 
5. Try to "force" the vulnerability using `dangerouslySetInnerHTML`. Learn why this prop name is so descriptive.

**Part 3: The Library Audit**
1. Run `npm audit` on your current project.
2. Review the report. It will likely show "Moderate" or "High" vulnerabilities in old dependencies.
3. Run `npm audit fix` to automatically update to safe versions.
4. Discuss why keeping your `node_modules` up-to-date is more important for security than writing secure code.

**Part 4: Automated Penetration Testing**
1. Download and install **OWASP ZAP** (an open-source security tool).
2. Point it at your local application's URL.
3. Run an "Automated Attack."
4. Review the generated report. It will likely flag missing security headers (like `X-Frame-Options` or `Content-Security-Policy`).
5. Use the `helmet` library in your Express app to instantly apply 15+ security headers to your site.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Client-side Validation. Validating that a user is an "Admin" on the frontend (React) is useless. A hacker can just open the DevTools and change the variable. All security checks MUST happen on the Backend.
- **Gotcha 2:** Hardcoded Secrets. Never commit your `.env` file containing database passwords to GitHub. Use GitHub Secrets or AWS Secrets Manager.

### Reflection Question
Why is "Security" considered a "Process" rather than a "Project" that you can finish?
