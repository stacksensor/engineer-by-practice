# Exercise 001 - The Internal Developer Portal (IDP)

### Objective
Enable the developers. Master the concept of **Platform Engineering** and the **Internal Developer Portal (IDP)**. Learn how a centralized platform (like **Backstage**) allows any developer to "Request a Database" or "Deploy a new App" in 1 minute, without needing to be an expert in Cloud infrastructure or Kubernetes.

### Core Concepts to Master
- **Platform Engineering:** Building the "Internal Cloud" for your company's developers.
- **Cognitive Load:** The "Mental effort" it takes for a developer to remember how to deploy their app. Platform Engineering is the effort to *reduce* this.
- **Golden Paths:** The "Standard, easy way" to build an app (e.g., 'If you pick React + Node, the platform handles everything automatically').
- **Self-Service:** Allowing developers to "Do it themselves" (e.g., click a 'New Database' button) without waiting for a ticket.
- **The Platform-as-a-Product:** Treating your developers as "Customers" and the platform as the "Product."

### Research Topics
- "Platform Engineering vs DevOps: The evolution"
- "What is an Internal Developer Portal (IDP)?"
- "Building a 'Golden Path' for your developers"
- "Spotify's Backstage: The most popular IDP"

---

### The Practical Challenge

**Part 1: The "Ticket" Nightmare**
1. You are a developer. You want a new Redis cache.
2. **Current Process:** 
   - Open a Jira ticket (Wait 2 days).
   - Ops team asks for details (Wait 1 day).
   - Ops team manually creates it in AWS (Wait 1 day).
3. Discuss: How long did this take? How much "Flow" was lost? (Answer: 4 days).

**Part 2: The "Self-Service" Dream**
1. You go to the **IDP Dashboard**. 
2. Click "Add Redis." 
3. The IDP runs a **Terraform** script in the background. 
4. The Redis is ready in 2 minutes.
5. Discuss: Why does this make a company 10x more productive?

**Part 3: The "Golden Path" Choice**
1. Your company supports:
   - **Node.js** (Golden Path - Fully automated).
   - **Anything else** (Manual - You are on your own).
2. Discuss: Why would 95% of developers choose Node.js? (Answer: Because it is the "Path of Least Resistance").

**Part 4: Identifying the "Cognitive" burden**
1. Research the "Cognitive Load" required to deploy a modern app manually:
   - (Answer: 1. Docker, 2. Kubernetes YAML, 3. IAM Roles, 4. VPC Networking, 5. CI/CD scripts).
2. Does the "IDP" eliminate these, or just "Hide" them? (Answer: It hides and automates them).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Silver Bullet" trap. Installing more tools (like Backstage) won't fix a broken culture. If your cloud engineers refuse to "Let go" of control, the portal will be useless.
- **Gotcha 2:** Hardcoding the platform. Don't build a platform that *only* works for one specific version of one specific cloud. Aim for flexibility.

### Reflection Question
Why is the "Internal Developer Portal" considered the "Next Step" after DevOps for large engineering organizations? (Answer: Because as a company grows, direct and manual DevOps work becomes impossible to manage for 1,000 developers).
