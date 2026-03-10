# Exercise 006 - Infrastructure as Code: Terraform & Pulumi

### Objective
Automate the cloud. Master **Infrastructure as Code (IaC)**—the art of using "Code" (YAML/HCL/Python/TS) to create servers, databases, and networks instead of clicking buttons in the AWS/GCP Console. Learn about **Terraform** (The most popular, YAML-like) and **Pulumi** (Using real programming languages) and understand the concept of "State" in IaC.

### Core Concepts to Master
- **The Declarative Approach:** "I want 5 servers." (You don't say 'HOW' to build them; you say 'WHAT' you want).
- **Terraform (HCL):** The HashiCorp Configuration Language. (Standard/Safe).
- **Pulumi:** Using Python/JS/Go/TS to define your servers. (Flexible/Powerful).
- **The State File:** A JSON file that tracks what actually exists in the cloud. NEVER DELETE THIS!
- **Plan vs Apply:** Previewing the changes (`terraform plan`) before actually spending money (`terraform apply`).
- **Resource Lifecycle:** Create -> Update -> Delete.

### Research Topics
- "Introduction to Terraform: Resources, Providers, and State"
- "Infrastructure as Code (IaC) vs manual configuration"
- "Pulumi vs Terraform: Programming vs Configuration"
- "The importance of the 'State' file in Terraform"

---

### The Practical Challenge

**Part 1: The "Manual" Drift (Scenario)**
1. You click "Create Database" in AWS.
2. 6 months later, you want a SECOND database just like it.
3. Discuss: How long does it take you to find all the "Secrets" and "Settings" you used 6 months ago? 
4. How does a **Terraform file** fix this? (Answer: You just copy-paste the code).

**Part 2: The "Plan" Step (Concept)**
1. Research **`terraform plan`**.
2. Discuss why a "Preview" is the most important part of IaC. 
3. (Answer: To prevent accidentally "Deleting" your production database because of a single typo!).

**Part 3: Terraform vs Pulumi**
1. Research the difference:
   - **Terraform:** `resource "aws_db" "name" { type = "t2.micro" }`.
   - **Pulumi:** `const db = new aws.rds.Instance("name", { instanceClass: "t2.micro" });`.
2. Discuss: Why would a Developer prefer **Pulumi** (using loops and 'if' statements) while an Ops Engineer might prefer **Terraform** (Simple text)?

**Part 4: Identifying the "Source"**
1. Research **`terraform-provider-aws`**. 
2. Discuss why you can use the SAME tool to manage AWS, GCP, Azure, and even Cloudflare.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Pushing State. If you commit your `terraform.tfstate` file to a public GitHub repo, your database passwords and private IP addresses will be visible to everyone. (Solution: Use a "Remote Backend" like S3).
- **Gotcha 2:** Only clicking the console. If you use IaC but *also* manually change things in the AWS Console, the next time you run `apply`, Terraform will "Undo" your manual changes. This is called "Resource Drift."

### Reflection Question
Why is "Infrastructure as Code" the only way to manage a company that has 1,000 servers in 5 different countries? (Answer: Because it is impossible for a human to remember the settings of 1,000 different machines without a 'Source of Truth').
