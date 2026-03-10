# Exercise 001 - Thinking like a Hacker: SecEng Intro

### Objective
Flip the script. Master the mindset of **Secure Software Engineering**. Learn the fundamental principles of **Security by Design**, and understand the Core Security Pillars: **Confidentiality**, **Integrity**, and **Availability** (The CIA Triad). Learn how to think from the "Attacker's" perspective while writing your next line of code.

### Core Concepts to Master
- **The CIA Triad:**
  - **Confidentiality:** Only the right people see the data.
  - **Integrity:** The data hasn't been changed by a hacker.
  - **Availability:** The system is up and working for users. CIA is a "Balance."
- **Security by Design:** Building security into the product from day 1, not as a "Fix" at the end.
- **Attack Surface:** The sum of all "Doors" where a hacker could try to enter (Every API, every input field, every open port).
- **Defense in Depth:** Using multiple layers of security (e.g., Firewall + Password + Database Encryption).

### Research Topics
- "The CIA Triad: Examples in daily life"
- "Security by Design vs Security through Obscurity"
- "The concept of 'Attack Surface' reduction"
- "What is a 'Zero-Day' vulnerability?"

---

### The Practical Challenge

**Part 1: The CIA Trade-off**
1. You have a "Top Secret" file.
2. To protect **Confidentiality**, you put it in a safe, buried 100 feet underground. 
3. Discuss: What happened to the **Availability** of that file? Is it useful anymore?
4. (Answer: No, if no one can access it, it has zero availability).

**Part 2: The Attack Surface Audit**
1. List all the "Doors" into a standard Todo app:
   - (Answer: 1. Sign-up form, 2. Login form, 3. 'Create Todo' API, 4. 'Delete Todo' API, 5. The Database port, 6. The Web Server port).
2. Discuss why "Deleting the 'Delete' API" is the most effective way to secure that feature.

**Part 3: Obscurity is NOT Security**
1. Your server is running on port `80`. Hackers find it instantly.
2. You move it to port `54321` and say "No one will ever look here!"
3. Research **Port Scanners** (like `nmap`). 
4. How long does it take for a bot to find your "Hidden" port? (Answer: Seconds).
5. Discuss why a "Hidden URL" is not a "Secure URL."

**Part 4: Identifying the "Attacker"**
1. Research the different types of hackers:
   - **Script Kiddie:** (No skill, uses tools).
   - **Internal Bad Actor:** (Employee).
   - **State Actor:** (Government).
2. Which one is the hardest to defend against? (Answer: State Actor).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Security through Obscurity" trap. Thinking that your secret keys are safe because they are "Hard to find" in a massive codebase. (Note: Use grep/search tools to find them!).
- **Gotcha 2:** Only focusing on the "Frontend." Hackers usually bypass your beautiful React UI and talk directly to your API with `curl` or `Postman`.

### Reflection Question
Why is security a "Process," not a "Product" you can buy? (Answer: Because as soon as you fix one vulnerability, attackers find a new way to break in).
