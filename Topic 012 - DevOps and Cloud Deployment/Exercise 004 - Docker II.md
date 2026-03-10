# Exercise 004 - Docker II (Dockerfiles)

### Objective
Move from using other people's images to building your own. Construct a `Dockerfile` to package your specific Node.js or React application into a portable, production-ready Docker image.

### Core Concepts to Master
- **The Dockerfile:** A plain-text configuration file containing the exact step-by-step instructions to assemble an image.
- **Base Images (`FROM`):** Starting your image from a pre-configured environment (e.g., `FROM node:18-alpine`).
- **Layers:** Docker caches every command inside the Dockerfile. Understanding how to order commands to optimize build speed.
- **Context:** The set of files on your machine that Docker "sees" when building an image.

### Research Topics
- "How to write a Dockerfile for Node.js"
- "Difference between COPY and ADD in Docker"
- "Optimizing Docker build layers"

---

### The Practical Challenge

**Part 1: The Basic Dockerfile**
1. In a directory with a simple `index.js` file (that logs "Hello Docker"), create a file named `Dockerfile` (no extension).
2. Add the following contents:
   ```dockerfile
   FROM node:18-alpine
   WORKDIR /app
   COPY index.js .
   CMD ["node", "index.js"]
   ```
3. Build the image: `docker build -t my-first-app .`
4. Run the image: `docker run my-first-app`. You should see "Hello Docker" in your terminal.

**Part 2: Managing Dependencies**
1. Initialize `npm init -y` and install a package (e.g., `chalk`). Update `index.js` to use it.
2. If you just copy `index.js`, the app will crash because `node_modules` is missing.
3. Update your Dockerfile to handle npm installs:
   ```dockerfile
   FROM node:18-alpine
   WORKDIR /app
   COPY package*.json ./
   RUN npm install
   COPY . .
   CMD ["node", "index.js"]
   ```
4. Rebuild. Notice that Docker now performs the installation during the build phase.

**Part 3: The .dockerignore**
1. On your host machine, you likely already have a heavy `node_modules` folder.
2. In Part 2, `COPY . .` accidentally copies your local (possibly Mac/Windows) `node_modules` into the Linux-based Docker image, which can cause architecture errors.
3. Create a `.dockerignore` file and add `node_modules`.
4. Run `docker build` again. Notice it runs faster as it ignores the local bloated folders.

**Part 4: Multi-Stage Builds (Optional Challenge)**
1. Build a React app. The build folder is only a few MBs, but the source code is 500MB+ with dev dependencies.
2. Research "Docker Multi-stage builds". 
3. Try to create a Dockerfile that uses Node to "build" the React app, then "copies" only the static `/dist` folder into a tiny Nginx image for serving. 
4. This results in a production image that is ~20MB instead of ~800MB.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Cache Busting. If you change your `index.js` but your `package.json` stays the same, Docker will skip the `npm install` step and reuse the cache. This is why we copy `package.json` *before* the rest of the source code.
- **Gotcha 2:** CMD vs RUN. `RUN` executes during the *build* process (to install stuff). `CMD` executes when the container *starts* (to run your app). 

### Reflection Question
Why should your production Docker images never contain development tools or the original source code files?