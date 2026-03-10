# Exercise 001 - Container Security Basics

### Objective
Learn to build secure foundations. Explore the fundamental practices of container security, including running as a non-root user, minimizing image size to reduce attack surface, and understanding how the container runtime isolates your processes from the host.

### Core Concepts to Master
- **The "Root" Problem:** Why running processes as root inside a container is a major security risk for the host system.
- **Distroless Images:** Minimal images that contain only your application and its dependencies, with no shell or package manager.
- **Read-Only Filesystems:** Locking down the container so that an attacker cannot write files or download malware.
- **Kernel Capabilities:** Dropping unnecessary Linux permissions (like `NET_ADMIN` or `SYS_ADMIN`) from your containers.

### Research Topics
- "Process isolation in Docker"
- "How to run Docker as non-root user"
- "What are distroless images?"
- "Docker security best practices 2024"

---

### The Practical Challenge

**Part 1: Identifying the Risk**
1. Run a standard container: `docker run -d --name risk-app nginx`.
2. Check the user running the process: `docker exec risk-app whoami`. (Result: `root`).
3. Discuss: If an attacker escapes this container, what level of access do they have to your computer/server?

**Part 2: Switching to Non-Root**
1. Create a `Dockerfile`.
2. Use a base image like `node:alpine`.
3. Add a dedicated system group and user: `addgroup -S appgroup && adduser -S appuser -G appgroup`.
4. Use the `USER appuser` command to switch contexts before the `CMD`.
5. Re-build and run. Verify `whoami` now returns `appuser`.

**Part 3: Read-Only Filesystem**
1. Run your container with the `--read-only` flag.
2. Try to create a file inside: `docker exec <container> touch /tmp/test`. It should fail.
3. Learn how to use "Tmpfs" mounts to allow writing to specific, temporary folders while keeping the rest of the app locked.

**Part 4: Dropping Capabilities**
1. Start a container and use `docker inspect` to see its default capabilities.
2. Re-run it using the `--cap-drop=ALL` flag and only manually adding back the specific one you need (e.g., `--cap-add=NET_BIND_SERVICE` if you are running a server on port 80).
3. Verify that the app still works but has zero extra permissions.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Permission Denied on Logs. If you switch to a non-root user, make sure that user has ownership (`chown`) of your application's log and data folders before starting the process.
- **Gotcha 2:** Alpine vs. Debian. Alpine-based images are tiny but use `musl` instead of `glibc`, which can occasionally cause compatibility issues with specific binary dependencies.

### Reflection Question
How does using a "Distroless" image make the life of a hacker significantly harder even if they manage to find a vulnerability in your code?
