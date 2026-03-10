# Exercise 003 - The "Make vs. Buy" Decision: Total Cost of Ownership (TCO)

### Objective
Weigh the options. Learn the most important "Business" skill for a Senior Engineer: **Total Cost of Ownership (TCO)**. Decide when to build a "Custom Tool" from scratch and when to pay $500/month for a "SaaS" (Software as a Service) to save your engineers' time.

### Core Concepts to Master
- **TCO (Total Cost of Ownership):** 
   - 1. **Initial Cost** (Build time).
   - 2. **Maintenance Cost** (Bug fixes).
   - 3. **Opportunity Cost** ("What *could* we have built instead?").
- **The "Engineer Salary" Math:** If a tool costs $500/month, and an engineer costs $10,000/month, why saving 2 hours of their time "Pays for the tool"?
- **Buy (SaaS):** Using **Auth0** or **Stripe** instead of writing your own bank connection.
- **Build (Custom):** Building your own "Proprietary AI" that the competition doesn't have.

### Research Topics
- "Calculating TCO: Build vs. Buy guide"
- "Opportunity Cost in Engineering: Choosing the right project"
- "Maintenance Debt: The cost of owning the code"
- "The SaaS Paradox: When 'Buying' becomes too expensive at scale"

---

### The Practical Challenge

**Part 1: The "Custom Auth" Disaster (Scenario)**
1. You want to build a "Login" system with MFA, OAuth, and LDAP.
2. **The "Build" math:** 
   - 2 Engineers * 3 Months = $60,000 in salary.
   - Maintenance: 1 Day/Month forever = $10,000/Year.
3. **The "Buy" math:** 
   - **Auth0** Costs $2,000/Year.
4. Discuss: **What is the "Payback Period" for building it yourself?** (Answer: 30 Years).
5. Discussion: Why is "Building Login" a bad use of your company's $100M budget?
6. Answer: Because "Login" is a **Utility**, not a **Competitive Advantage**.

**Part 2: The "Buy" Trap (Concept)**
1. You pay **Cloudflare** for "Bot Protection." It costs $0.05 per request.
2. You grow to **1 Billion requests** per month.
3. **The Bill:** $50,000,000. 
4. Research the **Exit Strategy**. 
5. Discuss: At what scale does it become "Cheaper" to build your own bot protection?
6. Answer: At the point where hiring 5 security engineers ($1M) is cheaper than the $50M bill.

**Part 3: The "Opportunity" Cost**
1. You have 10 engineers. 
2. 5 are fixing the "Custom Logging Tool" you built in 2012.
3. In that time, the competition builds a "New Mobile App" and steals 50% of your users.
4. Discuss: Did the "Free" logging tool actually cost the company $100M in lost users? (Answer: Yes).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "It's Easy!" An engineer says: "I can build that in a weekend." (Answer: They can build the *demo* in a weekend. They can't build the *10-year maintenance* in a weekend).
- **Gotcha 2:** Vendor Lock-in. If you "Buy," can you ever "Leave"? (Solution: Use **Open Standards** like SQL or OpenID Connect).

### Reflection Question
Why is "Not Writing Code" often the most valuable thing an Engineering Lead can do for their company's bank account? (Answer: Because every line of code written is a 'Liability' that must be paid for every year in maintenance).
