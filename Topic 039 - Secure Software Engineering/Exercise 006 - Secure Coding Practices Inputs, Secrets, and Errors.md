# Exercise 006 - Secure Coding Practices: Inputs & Secrets

### Objective
Clean up your code. Master **Secure Coding Practices**—the specific habits that every developer should follow to prevent vulnerabilities from being introduced. Learn how to handle **User Inputs** (Validation vs Sanitization), manage **Secrets** (Keys and Passwords), and write **Error Messages** that don't help hackers.

### Core Concepts to Master
- **Input Validation:** Rejecting "Bad" data (e.g., "The Age field MUST be a number between 1 and 120").
- **Input Sanitization:** Cleaning "Good" data (e.g., "The Name field can be any string, but I'm going to strip out any `<script>` tags").
- **Secret Management:** NEVER putting secrets in code. Use Environment Variables or a Secret Vault (like HashiCorp Vault or AWS Secrets Manager).
- **Graceful Failure:** Telling the user "Something went wrong" without showing the "Full Stack Trace" (which reveals your database structure and library versions).

### Research Topics
- "The difference between Validation and Sanitization"
- "How to use Pydantic (Python) or Zod (Typescript) for input validation"
- "Secrets in Environment Variables vs Secret Managers"
- "Designing secure error messages"

---

### The Practical Challenge

**Part 1: The Validation Challenge**
1. You have a "Zip Code" input.
2. A user types: `DROP TABLE users;`.
3. Discuss: If you only check "Is it a string?", the database might run the command. 
4. If you check "Is it exactly 5 digits?", the attack fails instantly.
5. (Answer: Validation is your first line of defense!).

**Part 2: The .env Mistake**
1. You create a `.env` file with `DATABASE_URL`.
2. You accidentally commit it to GitHub.
3. Discuss: Even if you delete it 1 minute later, it is still in the "Git History." 
4. Research: How do you "Scrub" a secret from your Git history? (Answer: `git filter-repo` or a tool like `BFG`).

**Part 3: The "Talking" Error**
1. Your app fails to connect to the DB.
2. Error (Insecure): `Error connecting to MySQL 8.0 at 10.0.0.5:3306. Access denied for 'admin'@'%'.`
3. Error (Secure): `Internal Server Error. Please contact support.`
4. Discuss: Why does the first error give a hacker a "Roadmap" of your internal network?

**Part 4: Identifying the source**
1. Research **OWASP Secure Coding Practices (Quick Reference Guide)**. 
2. Choose three rules that you are NOT currently following in your own code.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Validating on the Frontend only. A hacker can bypass your beautiful HTML5 validation with 1 line of `curl`. Always validate on the Backend!
- **Gotcha 2:** Password patterns in Logs. Be careful not to log "The whole request body" if it contains the word `password`. Many companies have accidentally leaked their entire user database into their own Loggly/Splunk logs.

### Reflection Question
Why is "Failing Closed" (blocking and logging) safer than "Failing Open" (allowing the action to happen and reporting an error) for security-sensitive code? (Answer: Because if the system crashes, it should fail into a "Secure" state, not a "Permissive" one).
