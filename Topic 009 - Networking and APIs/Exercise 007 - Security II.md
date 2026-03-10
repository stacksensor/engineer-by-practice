# Exercise 007 - Security II (XSS & Injection)

### Objective
Identify, exploit, and patch the two most critical code vulnerabilities in web applications. Master Cross-Site Scripting (XSS) payload interception and SQL Injection prevention mechanisms.

### Core Concepts to Master
- **Cross-Site Scripting (XSS):** Injecting malicious JavaScript payloads into a trusted website to steal user tokens or hijack sessions.
- **SQL Injection (SQLi):** Appending malicious SQL logic to raw database queries via user input fields to read, modify, or destroy entire database tables.
- **Data Sanitization:** Stripping dangerous characters from user input strings prior to processing or rendering.
- **Parameterized Queries:** Separating SQL code structures from string data fundamentally.

### Research Topics
- "OWASP Top 10 web vulnerabilities"
- "Preventing XSS in React vs Vanilla JS"
- "SQL Injection parameterized queries"

---

### The Practical Challenge

**Part 1: The XSS Vulnerability**
1. Construct a simple HTML page containing a text input labeled "Leave a comment".
2. Create an empty `div id="comments"` block below the input.
3. Write standard JavaScript to append the user's input directly into the DOM using `.innerHTML`.
4. Run the code. Type `Hello World`. It renders properly.
5. Now, type the payload `<script>alert('XSS Attack');</script>` into the comment box.
6. The browser executes the injected script block. You successfully exploited the application. 

**Part 2: Securing the DOM**
1. Update your JavaScript code. Replace `element.innerHTML = text` with `element.innerText = text`.
2. Input the exact same malicious payload `<script>` tag.
3. Note how the browser strictly displays the text string literally. It bypassed execution because `innerText` intrinsically sanitizes active DOM nodes.

**Part 3: The SQL Injection Crisis**
1. Set up a raw Node.js script. Build a mock SQL query string variable based natively on a user login attempt: `SELECT * FROM users WHERE username = '${req.body.username}' AND password = '${req.body.password}';`.
2. Submit the username `admin` and the password `admin`. The query executes normally.
3. Submit the username `admin' --`.
4. Note the output string generated: `SELECT * FROM users WHERE username = 'admin' --' AND password = '...';`.
5. The `--` symbol explicitly triggers an SQL comment sequence. The database ignores the entire password verification block. You bypassed authentication.

**Part 4: The Parameterized Defense**
1. Implement a parameterized query. Disconnect the data variable from the SQL command logic.
2. In standard libraries (like `pg` or `mysql`), map the inputs securely:
   ```javascript
   db.query('SELECT * FROM users WHERE username = $1 AND password = $2', [user, pass]);
   ```
3. Pass the malicious payload into the array. The database driver isolates the SQL command logic, explicitly interpreting `$1` as literal text. The attack fails safely.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Assuming front-end validation is sufficient security. Never trust front-end code. Attackers can bypass HTML validations using tools like Postman directly. Implement primary sanitization algorithms strictly on the backend APIs.
- **Gotcha 2:** Modern frameworks like React automatically sanitize `{variable}` JSX bindings against XSS injections. However, using `dangerouslySetInnerHTML={{__html: variable}}` explicitly bypasses this security shell.

### Reflection Question
If your framework automatically sanitizes input against XSS, why must you still explicitly scrub inputs against SQL injection?