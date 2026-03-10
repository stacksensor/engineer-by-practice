# Exercise 006 - CI/CD Fundamentals (Automation)

### Objective
Integrate automated deployment into your software lifecycle. Conceptualize a pipeline that automatically builds a Docker image and pushes it to a registry whenever your GitHub Actions test suite passes on the main branch.

### Core Concepts to Master
- **The Deployment Pipeline:** The stages of software delivery: Code -> Test -> Build -> Deploy.
- **Docker Registry (Docker Hub / ECR):** A remote repository where built images are stored securely before being pulled by production servers.
- **GitHub Actions Secrets:** Storing sensitive passwords and API keys (like your Docker Hub password) securely so the CI/CD scripts can use them without exposing them in plain text.
- **Continuous Delivery vs Deployment:** Knowing the difference between "ready to deploy" and "deployed automatically."

### Research Topics
- "GitHub Actions: Build and push to Docker Hub"
- "Understanding GitLab CI/CD vs GitHub Actions"
- "What is a container registry"

---

### The Practical Challenge

**Part 1: The Docker Hub Account**
1. Create a free account at [hub.docker.com](https://hub.docker.com).
2. Generate an "Access Token" (not your main password) in your security settings.
3. On your local machine, login using the CLI: `docker login -u your_username`. Paste your token when prompted.

**Part 2: Manual Push**
1. Tag an existing local image to match your Docker Hub username:
   `docker tag my-first-app your_username/my-first-app:v1.0.0`
2. Push it to the cloud: `docker push your_username/my-first-app:v1.0.0`.
3. Verify that the image now appears on the Docker Hub website. Anyone globally can now pull and run your application.

**Part 3: Secret Management**
1. In your GitHub repository, navigate to `Settings > Secrets and variables > Actions`.
2. Create two new secrets: `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN`.
3. Understand that once these are saved, they are encrypted and cannot be seen again, providing a secure way for your CI script to authenticate.

**Part 4: The Build Workflow**
1. Create a new GitHub Action workflow `.github/workflows/deploy.yml`.
2. Implement a "Docker Build and Push" job. Use the official `docker/build-push-action` from the GitHub marketplace.
   ```yaml
   steps:
     - uses: actions/checkout@v3
     - name: Login to Docker Hub
       uses: docker/login-action@v2
       with:
         username: ${{ secrets.DOCKERHUB_USERNAME }}
         password: ${{ secrets.DOCKERHUB_TOKEN }}
     - name: Build and push
       uses: docker/build-push-action@v4
       with:
         push: true
         tags: your_username/my-first-app:latest
   ```
3. Push the YAML file to GitHub and watch the pipeline automatically build and upload your application image to the registry.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Tagging Errors. If you forget to include your username in the tag, Docker Hub will reject the push with an "Access Denied" error, as you can only push to repositories you own.
- **Gotcha 2:** Failing Tests. Always make your "Build" job depend on your "Test" job. You should NEVER push a new image to the registry if the unit tests are failing.

### Reflection Question
Why is it safer to have a cloud server (GitHub Actions) build your Docker images rather than building them locally on your laptop and pushing them?