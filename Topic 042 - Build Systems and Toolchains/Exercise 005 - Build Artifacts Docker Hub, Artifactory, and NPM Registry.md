# Exercise 005 - Build Artifacts: Registries & Storage

### Objective
Ship the final product. Master **Build Artifacts**—the files that are the *result* of your build (Docker images, NPM packages, Java JAR files). Learn about the **Artifact Registry** (Storage for binaries) and understand why you should never "Build on Production" but rather "Build once, deploy many times."

### Core Concepts to Master
- **The Artifact:** The "Compiled/Packaged" output (e.g., `myapp.tar`, `index.js`, `image.docker`).
- **Artifact Registry (NPM Registry, Docker Hub, Artifactory):** The database where your company stores its internal binaries.
- **The Immutable Artifact:** Once a version (e.g., `1.2.3`) is pushed to the registry, it MUST never be changed. (Always increment to `1.2.4`).
- **Build Once, Deploy Often:** Building the binary once and sending it to "Dev," "Staging," and then "Prod." (Ensures the EXACT same code is tested and released).
- **Public vs Private Registries:** Sharing with the world vs Only sharing inside your company.

### Research Topics
- "What is an Artifact Registry? (e.g., JFrog Artifactory or AWS ECR)"
- "Docker Hub vs Private Docker Registries"
- "Publishing a private package to the NPM Registry"
- "The concept of 'Binary Repositories' for enterprise builds"

---

### The Practical Challenge

**Part 1: The "Build Once" Rule (Scenario)**
1. You have a "Dev" server and a "Prod" server.
2. Team A runs `npm install` on Dev.
3. Team B runs `npm install` on Prod 10 minutes later. 
4. Discuss: If a library just updated its code between the two installs, are the two servers running the same code? (Answer: No!).
5. How does a **Compiled Artifact** fix this? 
6. (Answer: You build the Zip/Docker on Dev, and "Copy" the *same file* to Prod).

**Part 2: The Registry Search**
1. Search **NPMJS.com** for a popular library (like `react`).
2. Look at the "Versions" tab. 
3. Discuss why you can still download `0.14.0` from 8 years ago. 
4. (Answer: The Registry is an "Archive" of every version ever released).

**Part 3: The Docker Image Artifact**
1. Research **AWS ECR (Elastic Container Registry)**. 
2. Discuss why it is the "Home" for all your Docker images. 
3. (Answer: When you want to scale a server, your cloud provider "Pulls" the image from the Registry, not from your laptop!).

**Part 4: Identifying the "Publish"**
1. Research the command:
   - `npm publish` (NPM).
   - `docker push` (Docker).
   - `cargo publish` (Rust).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Pushing Secrets. If you accidentally include a `.env` file inside your "NPM Package" or "Docker Image," anyone with access to the registry can steal your database keys. Use `.npmignore` or `.dockerignore`!
- **Gotcha 2:** Registry downtime. If your Registry (e.g., Docker Hub) is down, your "Auto-scaling" won't work, and you won't be able to "Deploy" even if your code is perfect. (Solution: Host a mirror of the registry inside your own cloud).

### Reflection Question
Why are "Artifacts" (Binaries) considered the "Real" version of the software, rather than the "Source Code"? (Answer: Because the source code needs a compiler and environment to run; the binary is 'Finished' and ready for the user).
