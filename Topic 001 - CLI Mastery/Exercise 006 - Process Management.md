# Exercise 006 - Process Management & Monitoring

### Objective
Master system-level control. Learn how to monitor running processes, manage background tasks, and troubleshoot resource-heavy applications using native CLI tools like `top`, `ps`, and `jobs`.

### Core Concepts to Master
- **Processes vs. Jobs:** Understanding the difference between a system-level process (PID) and a shell-level job (`fg`, `bg`).
- **Standard Signals:** Using `kill`, `killall`, and `HUP` to gracefully terminate or restart hanging applications.
- **Resource Monitoring:** Using `top`, `htop`, or `btm` to identify CPU/RAM bottlenecks in real-time.
- **Backgrounding (`&`):** Running a command in the background to free up your terminal for other tasks.

### Research Topics
- "Process management in Linux/Mac terminal"
- "Difference between SIGTERM and SIGKILL"
- "How to use screen or tmux for persistent sessions"
- "Monitoring CPU usage from command line"

---

### The Practical Challenge

**Part 1: Investigating Processes**
1. Run `top` (or `htop` if installed) to see the live list of system processes.
2. Identify the process ID (PID) of your terminal and your web browser.
3. Sort the list by "Memory Usage" to see which app is currently the heaviest.
4. Use `ps aux | grep <process_name>` to find a specific PID quickly.

**Part 2: Managing Background Jobs**
1. Run a long-running command (e.g., `sleep 100`).
2. Use `Ctrl+Z` to "Suspend" the job. 
3. Run `jobs` to see the suspended task.
4. Run `bg %1` to move it to the background. 
5. Finally, use `fg %1` to bring it back to the foreground and then `Ctrl+C` to kill it.

**Part 3: Handling Hanging Apps**
1. Create a "dummy" script that runs an infinite loop: `while true; do sleep 1; done`.
2. Run it and identify its PID.
3. Attempt to kill it using a "Graceful" signal: `kill <PID>`.
4. If it refuses to die, use the "Forced" signal: `kill -9 <PID>`.
5. Discuss why `kill -9` should be used as a last resort.

**Part 4: Terminal Multiplexing (Introduction)**
1. Research the `tmux` or `screen` command.
2. Create a new `tmux` session: `tmux new -s testing`.
3. Start a long-running task inside (e.g., `top`).
4. "Detach" from the session (`Ctrl+B` then `D`). Your terminal returns to normal, but the task is still running!
5. "Reattach" to the session: `tmux attach -t testing`. Observe that the task never stopped.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Accidentally killing the wrong process. Always double-check the PID before running `kill -9`. Using `killall <name>` is safer but can kill multiple instances of a program.
- **Gotcha 2:** Zombie Processes. Sometimes a process is "Dead" but still appears in the list. These are "Zombies" waiting for their parent process to acknowledge them. They don't use RAM, but they clutter the list.

### Reflection Question
How does using a multiplexer like `tmux` improve your productivity when managing remote servers over an SSH connection?
