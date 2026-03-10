# Exercise 007 - DevSecOps: Security in the Pipeline

### Objective
Security at the speed of code. Master **DevSecOps**—the practice of automating security checks directly in your CI/CD pipeline. Learn about **SAST** (Static Analysis Security Testing), **DAST** (Dynamic Analysis Security Testing), and **IAST** (Interactive Analysis) tools like **SonarQube**, **Snyk**, and **GitHub Advanced Security**.

### Core Concepts to Master
- **The Shift-Left approach:** Moving security checks as early as possible in the development lifecycle (i.e., when you run your unit tests).
- **SAST (Static Analysis):** Scanning your source code (no execution) for common patterns (e.g., hardcoded passwords, SQL injection vulnerabilities).
- **DAST (Dynamic Analysis):** Attacking a *running* app like a hacker (e.g., `ZAP Proxy` or `Burp Suite`).
- **Secrets Scanning:** Tools that watch every "Git Commit" and block it if you accidentally include an API key.
- **Vulnerability Scanning:** Scanning your Docker images (e.g., `Trivy` or `Snyk`) before you deploy them to production.

### Research Topics
- "SAST vs DAST: A comparison for developers"
- "GitHub Advanced Security: Code scanning and secret scanning"
- "Using Snyk or SonarQube in a CI/CD pipeline"
- "Shift-Left Security: Faster feedback for the developer"

---

### The Practical Challenge

**Part 1: The SAST Search**
1. You have a Python script: `import os; db_url = os.getenv("DB_URL", "postgres://admin:password123@localhost:5432/db")`.
2. A SAST tool (like **GitLeaks** or **Trufflehog**) scans this.
3. Discuss: How does the tool "know" that `postgres://...` is a secret credential? (Answer: Regular expressions and "Context" matching).

**Part 2: DAST vs SAST (Math)**
1. **SAST:** "Scans 1 million lines in 1 minute." Finds 50 "Potential" bugs. 20 of them are "False Positives."
2. **DAST:** "Runs for 1 hour against your test site." Finds 1 "Actual" SQL injection bug.
3. Discuss: Why are **both** necessary? (Answer: SAST finds the "Problem" (the line of code); DAST finds the "Exploit" (the actual way to hack it)).

**Part 3: The Docker Scan**
1. Research **Trivy**. 
2. Discuss: If your Node.js code is 100% secure, can a vulnerability in the underlying **Debian/Alpine** operating system (inside your Docker image) still allow a hacker to take over your server? 
3. (Answer: Yes! This is why scanning your "Container Image" is essential).

**Part 4: Identifying the "Block"**
1. Research **GitHub Secret Scanning**. 
2. Discuss what happens if you try to push a real **Stripe** or **AWS** key to a public GitHub repo. 
3. (Answer: GitHub blocks the push or sends an alert to the provider to instantly "Revoke" the key).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** False Positives. Automated tools often flags "Safe" code as "Dangerous." If you have 500 fake warnings, you will eventually ignore the "Real" warning.
- **Gotcha 2:** The "Pipeline Delay." If your security scan takes 45 minutes to run, developers will start "Skipping" it to save time. Keep your scans fast!

### Reflection Question
Why is "DevSecOps" considered the only way to manage security in a company that deploys 100 versions of their app every day? (Answer: Because human beings (security auditors) are too slow to keep up with that volume).
