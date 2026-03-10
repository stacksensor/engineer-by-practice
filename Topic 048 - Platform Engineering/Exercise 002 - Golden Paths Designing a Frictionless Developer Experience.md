# Exercise 002 - Golden Paths: Designing a Frictionless Developer Experience

### Objective
Smoothen the road. Learn to design **Golden Paths**—the "Easy way" to do the right thing—by creating templates and services that new developers can use to go from "Zero to PR" in 10 minutes.

### Core Concepts to Master
- **The "Golden Path":** The opinionated, battle-tested standard for your company (e.g., "Use **Go** + **Postgres** + **React**").
- **Platform vs. Product Engineering:**
   - **Product:** Builds the "Order Pizza" button for customers.
   - **Platform:** Builds the "Deploy Microservice" button for the Product team.
- **Service Scaffolding:** Tools like `npm init my-company-app` that generate 1,000 lines of "Boilerplate" code (Auth, Logging, Metrics) in 1 second.
- **Friction Audit:** Measuring why it takes 3 DAYS to get a "New Laptop" ready to code.

### Research Topics
- "Spotify Backstage: What is a Golden Path?"
- "Building a Scaffolder: The power of Yeoman or Hygen"
- "The Developer Experience (DX) Checklist: From Setup to Deployment"
- "Developer Portals: Centralizing the API surface area"

---

### The Practical Challenge

**Part 1: The "3-Day" Onboarding (Scenario)**
1. A new engineer joins. 
2. Day 1: Download Node.
3. Day 2: Can't find the DB password.
4. Day 3: Still trying to build the app.
5. Discuss: **How much money did the company LOSE in salary while this dev did 0 work?** (Answer: $2,000+).
6. **The Platform fix:** 
   - Research **DevContainers** or **GitHub Codespaces**.
   - Discuss: If they can "Click 1 button" and get a full coding environment in the browser in 60 seconds, how much money is saved?

**Part 2: The "Boilerplate" Scaffolder**
1. You have 10 services. Each has a different "Logging" format.
2. In an incident, you can't read the logs because they are all different.
3. **The Platform fix:** Build a **Scaffolder**. 
4. Discuss: If the "Library" is built *into* the template, why will 100% of future developers use the "Right" logging?
5. Answer: Because it's easier than writing it from scratch. **Pave the road with gold.**

**Part 3: The "Platform" Mindset (Concept)**
1. You are a Platform Engineer.
2. A Product engineer asks: "Can you create a S3 bucket for me?"
3. Research **Infrastructure as Code (IaC)**.
4. Discuss: Should you "Manualy click" the AWS console? Or write a **Terraform module**?
5. Answer: Neither. You should build a **Self-Service Portal** where the Dev clicks a button to get the bucket.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Silver" Paths. If your Golden Path is too strict (e.g., "You HAVE to use Java"), your best developers will quit to use Python elsewhere. (Solution: Allow "Off-roading" but with ZERO support from the platform team).
- **Gotcha 2:** Stale Templates. If your scaffold generates an old version of React (v15), you are creating "Instant Debt" for every new app. (Solution: **Bot updates** for your templates).

### Reflection Question
Why is "Self-Service" the ultimate goal of Platform Engineering? (Answer: Because if 1,000 developers have to wait for 1 Platform engineer to 'Click a Button', the whole company stops moving).
