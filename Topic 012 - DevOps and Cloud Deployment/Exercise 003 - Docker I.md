# Exercise 003 - Docker I (Images & Containers)

### Objective
"Containerize" your first application. Master the primary Docker CLI commands to download preconfigured environment images and run them as isolated, ephemeral containers on your local machine.

### Core Concepts to Master
- **The Docker Image:** A static, read-only file containing the application code, libraries, and dependencies (The "Class" in OOP terms).
- **The Docker Container:** A live, running instance of an image (The "Object" in OOP terms).
- **Docker Registry (Hub):** A centralized library (like GitHub but for images) where you can pull pre-built versions of Node, MySQL, or Nginx.
- **Port Mapping:** Connecting a port on your Host machine (e.g., 8080) to a port inside the isolated container (e.g., 80).

### Research Topics
- "Docker vs Virtual Machines key differences"
- "How to install Docker Desktop"
- "Docker pull, run, and ps commands explained"

---

### The Practical Challenge

**Part 1: The Hello-World Image**
1. Ensure Docker Desktop is installed and running.
2. Open your terminal and run your first container: `docker run hello-world`.
3. Read the output. Docker checked for the image locally, didn't find it, pulled it from Docker Hub, and executed it.
4. Verify the container has exited by running `docker ps -a`.

**Part 2: Running a Persistent Web Server**
1. Pull the official Nginx image: `docker pull nginx`.
2. Run it as a detached (background) container: `docker run -d --name my-server nginx`.
3. Try to visit `http://localhost`. Notice it doesn't work.
4. Why? The container's port 80 is isolated. Stop the container: `docker stop my-server`.
5. Remove the container: `docker rm my-server`.

**Part 3: The Port Bridge**
1. Run the server again, but this time map the ports:
   `docker run -d -p 8080:80 --name my-server nginx`
2. Visit `http://localhost:8080`. You should see the Nginx welcome page.
3. You have successfully bridged the gap between your physical machine and the containerized network.

**Part 4: Executing Into a Container**
1. You can "enter" a running container to explore its file system.
2. Use the `exec` command: `docker exec -it my-server /bin/bash`.
3. You are now inside the Ubuntu/Debian environment of the container. 
4. Navigate to `/usr/share/nginx/html`. 
5. Use `ls` and `cat` to view the `index.html` file. Notice how it matches the website you saw in the browser. 
6. Type `exit` to return to your host machine.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Name Conflicts. You cannot start two containers with the same `--name`. If you try, Docker will return an error. You must either use a different name or remove the old container first.
- **Gotcha 2:** Image Sprawl. Docker images take up significant disk space. Periodically run `docker system prune` to delete unused containers and old image layers that are no longer needed.

### Reflection Question
Why is "detaching" a container with the `-d` flag useful for building backend microservices?