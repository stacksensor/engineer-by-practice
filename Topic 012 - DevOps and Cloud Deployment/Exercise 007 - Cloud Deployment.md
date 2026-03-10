# Exercise 007 - Cloud Deployment (AWS/Heroku/Render)

### Objective
Go Live. Deploy your containerized application to a professional cloud provider (AWS, DigitalOcean, Render, or Heroku). Transition from "Localhost" to a live, public URL that users across the internet can access.

### Core Concepts to Master
- **IaaS vs PaaS:** Understanding the difference between managing a raw server (AWS EC2) versus a managed platform (Render/Heroku) that handles the server for you.
- **Environment Injection:** Passing production database credentials into your live cloud environment.
- **Log Management:** Monitoring the "Stdout" of your remote cloud containers to troubleshoot crashes.
- **DNS (Domain Name System):** The system that maps human-readable names (`myapp.com`) to the IP address of your cloud server.

### Research Topics
- "How to deploy a Docker container to Render"
- "Difference between AWS App Runner and EC2"
- "Setting up custom domains for web apps"

---

### The Practical Challenge

**Part 1: Choosing a Provider**
1. Select a provider with a free tier (Render, Fly.io, or Railway are recommended for beginners).
2. Connect your GitHub account to the provider. 
3. Create a "New Service" and select your repository.

**Part 2: The Build Specification**
1. Most modern cloud platforms automatically look for a `Dockerfile` in your repo.
2. Configure the deployment settings. Ensure the platform knows which "Port" your container is listening on (e.g., 3000).
3. If your app requires a database, provision a "Managed Postgres" instance on the same platform.

**Part 3: Secret Injection**
1. NEVER hardcode your live database URL in your code. 
2. Use the platform's "Environment Variables" section to add `DATABASE_URL`.
3. Update your app code to use `process.env.DATABASE_URL` if it exists, otherwise falling back to the local dev string.
4. Trigger a "Redeploy" and verify the app successfully connects to the remote database.

**Part 4: Monitoring and Persistence**
1. Find the "Logs" tab on your cloud dashboard.
2. Watch the logs as your app starts up. If it crashes, verify if it was a missing environment variable or a database connection timeout.
3. Access your public URL (e.g., `https://my-app.onrender.com`). Congratulations, you are now a full-stack cloud engineer.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The `PORT` variable. Many cloud platforms (like Heroku/Render) randomly assign a port to your container. You must configure your Express server to listen on `process.env.PORT || 3000` rather than strictly `3000`, or the deployment will fail health checks.
- **Gotcha 2:** Cold Starts. Free cloud tiers often "sleep" if they don't receive traffic for 15 minutes. The first request after a sleep period may take 30+ seconds to respond. This is normal for free plans.

### Reflection Question
Why is a "Platform as a Service" (PaaS) like Render or Heroku often preferred for startup prototypes over a "Infrastructure as a Service" (IaaS) like AWS EC2?