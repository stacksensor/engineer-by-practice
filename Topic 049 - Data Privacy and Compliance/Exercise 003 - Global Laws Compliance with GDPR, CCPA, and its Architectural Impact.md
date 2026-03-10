# Exercise 003 - Global Laws: Compliance with GDPR, CCPA, and its Architectural Impact

### Objective
Scale the rules. Learn how to architect a global system that obeys the **GDPR (Europe)** and **CCPA (California)**. Understand why you must "Tag" every user data row with their "Region" to move or delete it.

### Core Concepts to Master
- **GDPR:** "Personal Data" belongs to the user, not the company.
- **The "Right to be Forgotten":** If a user clicks "Delete," you MUST find every backup, log, and disk with their email in 30 days.
- **Data Residency:** Why "European" data can never live on a "USA" server without a legal contract.
- **Privacy by Design:** Building the "Delete" button *before* you build the "Collect" button.
- **Penalties:** $20M or 4% of Global Revenue. 

### Research Topics
- "GDPR vs CCPA: The technical differences"
- "Implementing 'The Right to be Forgotten' in a SQL database"
- "AWS Region Strategy for GDPR compliance"
- "Data Tagging for Privacy Compliance"

---

### The Practical Challenge

**Part 1: The "Legal" Disaster (Scenario)**
1. A user from France clicks "Delete my account."
2. **Without a Plan:** You delete them from the Database.
3. **The Audit:** The regulator finds their email in your **CloudWatch Logs** and **S3 Backups**.
4. **The Fine:** $1M.
5. Discuss: Does "Delete" mean just the row? (Answer: No. It means EVERY trace of the human).
6. **The Architectural fix:** 
   - Research **Data Tagging**.
   - Discuss: If every log has a `userId` tag, can a robot delete all logs for `user_123`?

**Part 2: The "Residency" Rule**
1. Research **Data Residency**. 
2. Discuss why a German user's data should stay in the `eu-central-1` (Frankfurt) AWS region.
3. Answer: Because laws change based on where the *atoms* (the servers) are.
4. Discussion: If you have a "Global" company with 1 database in the US, how do you handle users from 50 countries?

**Part 3: The "Opt-Out" (Concept)**
1. Research **CCPA (California)**. 
2. Discuss the "Do Not Sell" link.
3. Discussion: If you share data with a "Tracking Pixel" (Facebook/Google), are you technically "Selling" it?
4. Answer: Under CCPA, yes. **You must have a 'Switch' in the code to stop sending the pixel.**

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Secondary" Database. You delete a user from the API, but they still exist in your **Data Warehouse (BigQuery)** for reports. (Solution: Sync the "Delete" event!).
- **Gotcha 2:** Log Redaction. Accidentally logging an email in a "Debug" message. (Solution: Use **Regex Filter** to mask emails in logs).

### Reflection Question
Why are "Data Privacy Laws" the #1 reason why microservices are harder to build than monoliths? (Answer: Because you have to 'Delete' the user from 50 different microservices simultaneously).
