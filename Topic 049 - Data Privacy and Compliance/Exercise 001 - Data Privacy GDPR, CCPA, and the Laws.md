# Exercise 001 - Data Privacy: GDPR, CCPA, and the Laws

### Objective
Respect the user's data. Master the two most important data privacy laws: **GDPR** (Europe) and **CCPA** (California). Learn the principles of **Consent**, **Access**, and **Deletion**, and understand why a single mistake in "Data Privacy" can result in millions of dollars in fines for your company.

### Core Concepts to Master
- **GDPR (General Data Protection Regulation):** The European standard for privacy.
- **CCPA (California Consumer Privacy Act):** The California standard (similar to GDPR).
- **Personally Identifiable Information (PII):** Anything that can identify a specific human (e.g., Name, Email, IP Address, Location, SSN).
- **The "Right to be Forgotten":** A user's legal right to ask you to "Delete every single trace of me" from all your databases and logs.
- **Data Processor vs Data Controller:** You (The app) vs The Cloud (AWS).

### Research Topics
- "GDPR Principles: Transparency, Purpose, Minimization"
- "What counts as PII (Personally Identifiable Information)?"
- "The 'Right to Access' (SAR - Subject Access Request)"
- "Privacy by Design: Building it into the code"

---

### The Practical Challenge

**Part 1: The PII Identification Audit**
1. You have a "User" table in your database.
2. Columns: `id, first_name, last_name, email, age, ip_address, latitude, longitude, height, favorite_color`.
3. Which of these are **PII**?
   - (Answer: First Name, Last Name, Email, IP Address, Latitude, Longitude).
4. Discuss: Is "Favorite Color" PII? (Answer: No, it doesn't identify you... unless you are the only person in a small town who likes 'Neon Purple').

**Part 2: The "Delete Me" Challenge**
1. A user clicks "Delete My Account (GDPR)."
2. You delete their row from the `users` table. 
3. Discuss: Is their data still in:
   - Your database backups (from 3 days ago)?
   - Your S3 logs?
   - Your "Deleted Users" archive? 
4. If you don't delete it EVERYWHERE, you are in violation of GDPR. How does a **UUID** make this easier?

**Part 3: The "Residency" Problem**
1. A German user's data is sent to a server in Virginia, USA.
2. Discuss why this might be a **GDPR violation** depending on the current "Privacy Shield" laws. 
3. Research: What is **Data Residency**? (Answer: Keeping the data inside the physical borders of a country).

**Part 4: Identifying the regulation**
1. Which law for:
   - "A health app where I store my blood pressure" (Answer: HIPAA).
   - "A bank where I store my credit card" (Answer: PCI-DSS).
   - "A social network for any European user" (Answer: GDPR).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** PII in URLs. Never put an email address in a URL (`/users/alex@gmail.com`). URLs are saved in "Browser History" and "Web Server Logs" in plain text, which is an instant security and privacy failure.
- **Gotcha 2:** The "Audit" trap. To be compliant (SOC2/ISO), you must have "Audit Logs" of who looked at a user's data. If you have no logs, you cannot prove that you are being "Private."

### Reflection Question
Why is "Data Collection" now considered a "Liability" (like a dangerous chemical) rather than an "Asset" for many companies? (Answer: Because if you don't have it, you can't be sued or hacked for it!).
