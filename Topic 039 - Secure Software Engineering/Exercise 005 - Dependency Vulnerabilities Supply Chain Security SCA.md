# Exercise 005 - Dependency Vulnerabilities: Supply Chain

### Objective
Watch your back. Master **Software Composition Analysis (SCA)**—the art of finding and fixing vulnerabilities in the 3rd-party libraries (NPM, Pip, Go, etc.) your app depends on. Understand the **Supply Chain Attack** and learn how a hacker can "Poison" a popular package to steal data from 10,000 different companies.

### Core Concepts to Master
- **The Supply Chain:** Your code + The frameworks you use + The libraries *those* frameworks use.
- **Transitive Dependency:** A library used by another library that you use. You might not even know it's there!
- **SCA (Software Composition Analysis):** Tools that scan your `package.json` or `requirements.txt` for known vulnerabilities (CVEs).
- **SemVer Pinning:** Locking your versions (e.g., `1.2.3` instead of `^1.2.0`) to prevent a "Bad version" from being installed automatically.
- **Lockfiles:** `package-lock.json` or `poetry.lock`. Ensuring every developer (and the server) has the EXACT same bytes.

### Research Topics
- "NPM Audit: Finding vulnerabilities in your Javascript app"
- "The Log4j vulnerability (Log4Shell) and its impact"
- "What is a CVE (Common Vulnerabilities and Exposures)?"
- "The 'Typo-squatting' attack in NPM/PyPI"

---

### The Practical Challenge

**Part 1: The `npm audit` Test**
1. Create a new folder. Run `npm init -y`.
2. Install an old, vulnerable library: `npm install lodash@4.17.4`.
3. Run `npm audit`.
4. Observe the report. How many vulnerabilities were found? 
5. What is the "Severity" level? (High/Critical).
6. Run `npm audit fix` and see if it can solve the problem for you.

**Part 2: The "Transitive" Disaster**
1. Research the **Log4Shell** vulnerability from 2021.
2. Discuss why it was so dangerous: Most people didn't *know* they were using the Log4j library; it was "Hidden" inside 1,000 other Java libraries they were using.
3. How many companies were affected globally? (Answer: Millions).

**Part 3: The "Typo-squatting" Test**
1. You want to install `request`. You accidentally type `npm install reqeust`.
2. Discuss: A hacker can register the "Typo" name and put a virus inside it. 
3. Research: Does NPM or PyPI have a policy for this? (Answer: Yes, but thousands still slip through every month).

**Part 4: Identifying the "Lock"**
1. Discuss: Why should you NEVER delete your `package-lock.json` file? 
2. (Answer: Without it, your laptop and your production server might install different versions of a library. A bug that doesn't exist on your laptop could crash the server!).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Broken" Fixes. Sometimes `npm audit fix` will upgrade a library to a newer version that "Breaks" your code. You must always test after a security fix.
- **Gotcha 2:** Ignoring the "Moderate" warnings. Small vulnerabilities are often used as "Step 1" of a much larger attack. Fix everything you can!

### Reflection Question
Why is the "Supply Chain" now considered the #1 attack surface for modern software companies? (Answer: Because it's easier to hack 1 popular open-source library than it is to hack 1,000 individual company firewalls).
