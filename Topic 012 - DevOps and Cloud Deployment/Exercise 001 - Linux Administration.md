# Exercise 001 - Linux Administration

### Objective
Graduate from local GUIs to the remote command line. Internalize the foundational Linux commands required to navigate, manage permissions, and troubleshoot live production servers (Ubuntu/Debian) where your applications will eventually reside.

### Core Concepts to Master
- **The File System:** Understanding the root-based hierarchy (`/var`, `/etc`, `/home`, `/tmp`).
- **Owner & Permissions:** Mastering `chmod` and `chown` to secure sensitive application configuration files.
- **Process Management:** Using `top`, `ps`, and `kill` to monitor and terminate hanging server processes.
- **SSH (Secure Shell):** Establishing encrypted terminal tunnels to remote virtual machines via identity keys.

### Research Topics
- "Basic Linux command line cheatsheet"
- "Understanding Linux file permissions (rwx)"
- "How to use SSH keys for authentication"

---

### The Practical Challenge

**Part 1: Navigation and Manipulation**
1. Open your terminal (or a remote Ubuntu terminal via WSL/Cloud Shell).
2. Practice absolute vs relative paths. Navigate to `/var/log` and back to your `$HOME`.
3. Create a directory named `app-deploy`. Inside, create a file named `config.env`.
4. Use `ls -la` to view the hidden attributes. Notice the default permissions (e.g., `-rw-r--r--`).

**Part 2: Permission Enforcement**
1. Secure your `config.env` file. Change the permissions so that ONLY the owner can read/write it.
2. Use `chmod 600 config.env`.
3. Verify the change. Try to read the file using `cat` from a different (mock) user if available, or notice the string `rw-------`.
4. Learn to use `sudo`. Try to create a file inside `/etc/` and observe the "Permission Denied" error until you prepend `sudo`.

**Part 3: Stream Redirection and Grep**
1. Master the pipe `|` and `grep` combo.
2. List all running processes: `ps aux`.
3. Chain the command to find only your terminal/shell process: `ps aux | grep zsh` (or `bash`).
4. Practice output redirection. Save the list of running processes to a file: `ps aux > processes.txt`.
5. Append text to an existing file using `>>`.

**Part 4: Networking and Connectivity**
1. Check your local IP configuration using `ip addr` (or `ifconfig`).
2. Test connectivity to a remote server using `ping google.com`.
3. Use `curl -I http://google.com` to inspect the raw HTTP headers of a website via the command line.
4. Prepare an SSH key using `ssh-keygen`. Understand that the "Private Key" never leaves your machine, while the "Public Key" is what you upload to the server.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The `rm -rf /` Nightmare. The `-r` flag stands for recursive and `-f` for force. Never run `rm -rf` on a directory unless you are absolutely certain of its path, as there is no "Trash Can" in the Linux terminal.
- **Gotcha 2:** Case Sensitivity. Unlike Windows, Linux treats `File.txt` and `file.txt` as two completely separate, unique files.

### Reflection Question
Why are server-side applications almost exclusively hosted on Linux-based operating systems rather than Windows or macOS?