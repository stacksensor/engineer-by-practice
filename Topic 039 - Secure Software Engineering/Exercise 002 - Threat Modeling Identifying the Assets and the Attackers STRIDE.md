# Exercise 002 - Threat Modeling (STRIDE)

### Objective
Be prepared. Master **Threat Modeling**—the process of identifying potential security threats at the design phase. Learn the **STRIDE** model (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) and understand how to draw a **Data Flow Diagram (DFD)** to find "Choke Points" in your app's security.

### Core Concepts to Master
- **STRIDE Framework:**
  - **S**poofing: Pretending to be someone else.
  - **T**ampering: Changing data in the database.
  - **R**epudiation: Denying that you did an action (no audit log).
  - **I**nformation Disclosure: Seeing data you shouldn't see.
  - **D**enial of Service: Crashing the app for others.
  - **E**levation of Privilege: A regular user becoming an Admin.
- **The Asset:** What are we protecting? (e.g., Credit cards, Health data, Your source code).
- **The Trust Boundary:** The line between "Safe" code (inside your server) and "Dangerous" code (the internet).

### Research Topics
- "STRIDE Threat Model: One example for each letter"
- "How to draw a Data Flow Diagram (DFD) for security"
- "Identifying trust boundaries in a cloud app"
- "Threat modeling for a simple 'Login' form"

---

### The Practical Challenge

**Part 1: The STRIDE Audit**
1. You are building a "Comment System" for a blog.
2. Apply the STRIDE model:
   - **Spoofing:** Can I post a comment as "The Admin"? 
   - **Tampering:** Can I change someone else's comment after it's posted?
   - **Repudiation:** If I delete a user's account, can the system prove *I* did it?
   - **Information Disclosure:** Can I see the email addresses of every commenter by looking at the page source?
   - **Denial of Service:** Can I post 1,000,000 comments in 1 second to crash the DB?
   - **Elevation of Privilege:** Can I add a hidden field to my comment that makes me a Moderator?

**Part 2: The DFD Drawing**
1. Draw a diagram:
   - User -> **[Internet]** -> API Gateway -> **[Firewall]** -> User Service -> Database.
2. Identify the "Trust Boundaries." Trace where the data is "Untrusted" (outside) and "Trusted" (inside).
3. Discuss why "Untrusted" data should ALWAYS be validated before crossing a boundary.

**Part 3: The Mitigation Plan**
1. For the "Comments" DoS attack (from Part 1), how do you fix it? 
2. (Answer: Rate limiting, CAPTCHA, or mandatory login).

**Part 4: Identifying the "Repudiation"**
1. Research **Audit Logs**. 
2. Discuss why a log that says `Someone changed the price` is useless compared to one that says `Admin Alex changed price to $50 at 2:03 PM`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-modeling. Don't spend 3 weeks threat modeling a "Hello World" app. Focus on the data that matters (Users/Money/Secrets).
- **Gotcha 2:** Only focusing on external threats. Statistics show that many major security breaches are caused by "Internal" users or disgruntled employees.

### Reflection Question
Why is "Threat Modeling" the most valuable activity a software engineer can do before they start writing code for a new feature? (Answer: Because fixing a security flaw in a design is 100x cheaper than fixing it in a live database).
