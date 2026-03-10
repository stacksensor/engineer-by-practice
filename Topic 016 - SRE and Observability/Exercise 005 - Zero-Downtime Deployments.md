# Exercise 005 - Zero-Downtime Deployments

### Objective
Master "Invisible Updates." Implement deployment strategies like Blue-Green and Canary releases to ensure your users never see a 404 or a "Maintenance" page while you are updating your code. Learn how to safely "Roll Back" in seconds if a new version contains a critical bug.

### Core Concepts to Master
- **Blue-Green Deployment:** Having two identical environments (Blue=Old, Green=New). You route traffic to Blue, deploy to Green, test it, and then "flip the switch" on the load balancer to Green.
- **Canary Release:** Slowly rolling out a new version to a small percentage (e.g., 5%) of users first to gather metrics before completing the update for everyone.
- **Rolling Update:** Updating one server instance at a time in a cluster so the total capacity remains partially available throughout the process.
- **The Load Balancer Pivot:** Using the Gateway (Nginx/AWS ELB) as the final arbiter of which code version the user sees.

### Research Topics
- "Blue-Green vs Rolling vs Canary deployment"
- "How Kubernetes handles zero-downtime updates"
- "Implementing a Blue-Green switch with Nginx"
- "Feature flags for safe deployments"

---

### The Practical Challenge

**Part 1: The Multi-Version Cluster**
1. Use Docker Compose to launch two identical versions of your app: `v1` (Blue) and `v2` (Green).
2. Configure an Nginx Load Balancer to point only to Blue (port 3001).
3. Visit the public URL. You are seeing the "Old" version of the site.

**Part 2: The Blue-Green Switch**
1. Confirm that `v2` is running correctly on its own port.
2. Update the Nginx config to point to Green (port 3002).
3. Run `nginx -s reload`.
4. Refresh the page. You should instantly see the "New" version. 
5. Congratulations! If you noticed a bug, you could flip the config back to Blue in milliseconds. This is Zero-Downtime.

**Part 3: The Canary rollout**
1. Many systems use "Weights" to distribute traffic.
2. Configure Nginx (or a cloud provider) to send 90% of traffic to Blue and 10% to Green.
3. Refresh the page many times. You should see the new version only about once every ten refreshes.
4. This allows you to monitor your "Error Logs" (Sentry/ELK) for that 10% of users to ensure the new version is stable.

**Part 4: Database Schema Migrations**
1. The hardest part of Zero-Downtime is the database.
2. If you delete a column in your DB, the "Old" Blue version will crash instantly.
3. Research the "Expand and Contract" pattern:
   - Step 1: Add a new column.
   - Step 2: Deploy code that writes to BOTH columns.
   - Step 3: Deploy code that reads only from the NEW column.
   - Step 4: Delete the OLD column.
4. Discuss why this 4-step process is the ONLY way to safely update a database in a zero-downtime environment.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Hardcoded IP Addresses. If you use hardcoded IPs in your load balancer, your Blue-Green switch will involve manual editing and downtime. Always use DNS names or Service Discovery.
- **Gotcha 2:** User Session Loss. If sessions are stored on the server's disk, flipping from Blue to Green will log out every single user. This is why centralized session stores (Redis) are mandatory for these patterns.

### Reflection Question
Why is the "Canary" release considered safer for high-traffic platforms (like Facebook or Netflix) than a full Blue-Green switch?
