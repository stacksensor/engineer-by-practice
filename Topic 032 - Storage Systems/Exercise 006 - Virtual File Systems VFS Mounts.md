# Exercise 006 - Virtual File Systems (VFS) & Mounts

### Objective
One interface for all. Master the **Virtual File System (VFS)** layer. Learn how Linux/Mac allows `ls` and `cat` to work identically whether the data is on a local SSD, a USB drive, a Network share (NFS), or even a "Fake" disk like `/proc`. Understand the **Mount Point** and the global hierarchy.

### Core Concepts to Master
- **The VFS Layer:** The kernel abstraction that provides a standard "File API" (`open`, `read`, `write`) to all applications, regardless of the underlying storage.
- **Mounting:** Attaching a physical partition (e.g., `/dev/sdb1`) to a specific directory in your hierarchy (e.g., `/mnt/backup`).
- **Pseudo-filesystems:** "Files" that don't exist on disk but represent kernel information (e.g., `/proc` for processes, `/sys` for hardware).
- **FUSE (Filesystem in Userspace):** A trick that allows you to write a filesystem in a high-level language like Python or JS and "Mount" it as a real folder.

### Research Topics
- "The Linux Virtual File System (VFS) architecture"
- "What is /proc and why is it called a 'Pseudo' filesystem?"
- "Mounting a remote disk via NFS or SSHFS"
- "How FUSE works for developers"

---

### The Practical Challenge

**Part 1: The Mount Map**
1. Use `mount` or `df -h`. 
2. Identify the various filesystems currently active. 
3. Distinguish between "Real" disks (like `ext4` or `apfs`) and "Memory" disks (like `tmpfs` or `sysfs`).

**Part 2: The Magic /proc**
1. On Linux: `cat /proc/cpuinfo`. On Mac: `sysctl -n machdep.cpu.brand_string`.
2. Notice how the computer treats "Hardware information" as if it were a text file.
3. Discuss: Why is "Everything is a file" the most powerful philosophy in UNIX?

**Part 3: Mounting a USB/Disk (Manual)**
1. Research the command `mount -t <type> <device> <directory>`.
2. Discuss: What happens to the files existing in the directory `/mnt/test` BEFORE you mount a disk over it? (Answer: They become "Hidden" until you unmount).

**Part 4: The FUSE Concept (Conceptual)**
1. Research **SSHFS**. 
2. Discuss how you can "Mount" a folder from a server in London as if it were a local folder on your laptop in NYC. 
3. How does the VFS handle the latency of the network?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Device is busy." You cannot unmount a disk if a program (like your terminal) is "sitting" in that folder. You must `cd` out of the drive first.
- **Gotcha 2:** Mount order. If you mount `/home` first and then `/`, you might break the system. The hierarchy matters.

### Reflection Question
How does the VFS allow a Java or Python program to work on both Windows and Linux without rewriting its file-saving code? (Answer: Abstraction of the underlying filesystem logic).
