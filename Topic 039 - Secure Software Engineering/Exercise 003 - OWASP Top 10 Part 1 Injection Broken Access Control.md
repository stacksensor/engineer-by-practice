# Exercise 003 - OWASP Top 10 Part 1: Injection & Access Control

### Objective
Stop the bleeding. Master the first half of the **OWASP Top 10**—the industry-recognized list of the most critical security risks to web applications. Focus on #1: **Injection** (SQL, OS, Script) and #2: **Broken Access Control**. Learn how a single "Vulnerable" string can allow any user to delete your entire database.

### Core Concepts to Master
- **Injection:** An attacker sends "Data" that the server thinks is a "Command" (e.g., `' OR 1=1 --`).
- **SQL Injection (SQLi):** Attacking a database through a URL parameter or a form.
- **Parametrized Queries:** The only safe way to talk to a database. (Separate the "Command" from the "Data").
- **IDOR (Insecure Direct Object Reference):** A type of Broken Access Control where you can see another user's data by changing a number in the URL (`/orders/123` to `/orders/124`).

### Research Topics
- "SQL Injection basics (The 'OR 1=1' trick)"
- "Using prepared statements (parametrized queries) in Python/JS"
- "What is IDOR and how to prevent it"
- "Horizontal vs Vertical privilege escalation"

---

### The Practical Challenge

**Part 1: The SQLi Exploit (Conceptual)**
1. You have a query: `SELECT * FROM users WHERE email='` + `req.body.email` + `'`.
2. A hacker types this in the "Email" box: `' OR 1=1 --`.
3. The server runs: `SELECT * FROM users WHERE email='' OR 1=1 --'`.
4. Discuss: Why does this let the hacker log into YOUR account? 
5. (Answer: `1=1` is always true, and `--` comments out the rest of the query).

**Part 2: The "Prepared" Fix**
1. Research how to write the same query using a library that separates the data:
   - `db.query("SELECT * FROM users WHERE email = ?", [req.body.email])`.
2. Discuss why this is 100% safe from SQLi. (Answer: The database knows that the string inside the `[]` is just data, not a command).

**Part 3: The IDOR Audit**
1. You have a URL: `https://bank.com/api/statements/12345`.
2. You change it to: `https://bank.com/api/statements/12346`.
3. If you can see the other user's bank statement, which security rule was broken? (Answer: Broken Access Control).
4. How do you fix it? (Answer: The server must check: `WHERE id=12346 AND user_id=MY_ID`).

**Part 4: Identifying the "Elevation"**
1. Research the difference between:
   - **Horizontal:** (Seeing another user's data).
   - **Vertical:** (A user becoming an Admin).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Assuming an ORM (like Sequelize or Prisma) makes you 100% safe. If you use "Raw SQL" strings inside your ORM, you are still vulnerable to injection!
- **Gotcha 2:** Only protecting the "ID" in the URL. Hackers also check "Headers," "Cookies," and "POST Body" for IDOR vulnerabilities.

### Reflection Question
Why is "Never Trust User Input" the most important sentence in all of software engineering? (Answer: Because any user input can be a hidden command for your system).
