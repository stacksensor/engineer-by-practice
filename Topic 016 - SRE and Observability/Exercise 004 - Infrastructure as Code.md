# Exercise 004 - Infrastructure as Code (Terraform)

### Objective
Automate your cloud hardware. Stop manually clicking "Create Server" in the AWS or DigitalOcean dashboard. Use Terraform to define your infrastructure (Servers, Databases, Networks) in code, allowing you to version, replicate, and destroy entire environments with a single command.

### Core Concepts to Master
- **HCL (HashiCorp Configuration Language):** The declarative language used by Terraform to describe the "Desired State" of your cloud resources.
- **The State File:** A JSON file where Terraform tracks exactly what it has created in your cloud account. (Never delete this!).
- **Providers:** Plugins that allow Terraform to communicate with specific cloud APIs (AWS, Azure, GCP, Cloudflare).
- **Execution Plan:** Running `terraform plan` to see exactly what changes will be made BEFORE they are applied.

### Research Topics
- "What is Infrastructure as Code (IaC)?"
- "Terraform vs CloudFormation vs Ansible"
- "Terraform project structure best practices"
- "Managing Terraform state in a team"

---

### The Practical Challenge

**Part 1: The First Resource**
1. Install the Terraform CLI on your machine.
2. Choose a provider (DigitalOcean or AWS). 
3. Create a `main.tf` file. Define a single, tiny server (an EC2 instance or a Droplet).
   ```hcl
   resource "digitalocean_droplet" "web" {
     name   = "tf-server"
     size   = "s-1vcpu-1gb"
     image  = "ubuntu-22-04-x64"
     region = "nyc1"
   }
   ```
4. Run `terraform init` to download the provider plugin.

**Part 2: Planning and Applying**
1. Run `terraform plan`. It should say "1 to add, 0 to change, 0 to destroy."
2. Run `terraform apply`. Watch as your real cloud dashboard shows a new server being created in real-time.
3. Observe how Terraform uses an API key (passed via environment variable) to authenticate.

**Part 3: Modifying Infrastructure**
1. Change the `size` of your server in the `main.tf` file (e.g., from `1gb` to `2gb`).
2. Run `terraform plan`. Observe that Terraform identifies that it must *replace* the server to change its hardware size.
3. Run `terraform apply`. Watch the old server vanish and a new, larger one appear. This is the "Immutable Infrastructure" mindset.

**Part 4: Destroying Environments**
1. When you are finished testing, run `terraform destroy`.
2. Observe how Terraform uses the "State File" to find everything it created and delete it instantly.
3. This is how billion-dollar companies spin up entire "Staging" environments for testing and tear them down at the end of the day to save money.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Secret Leaks. Never commit your `terraform.tfstate` or your API keys to GitHub. The state file can contain sensitive passwords and credentials. Always use a `.gitignore` or a "Remote State" backend (like S3 or Terraform Cloud).
- **Gotcha 2:** State Locking. If two developers try to run `terraform apply` at the same time, the state file can become corrupted. Use a backend that supports "Locking" (like DynamoDB).

### Reflection Question
How does Infrastructure as Code (IaC) reduce the risk of "Human Error" compared to configuring a production server manually via a web interface?
