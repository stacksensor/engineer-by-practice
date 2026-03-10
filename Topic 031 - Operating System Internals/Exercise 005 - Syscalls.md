# Exercise 005 - Syscalls (The Kernel API)

### Objective
Cross the barrier. Master **System Calls (Syscalls)**—the standard way for "User Space" code (your Python/JS/C code) to ask the "Kernel" to perform privileged tasks like reading a file, sending a network packet, or starting a new process. Learn about the **Mode Switch** and how it protects the stability of the computer.

### Core Concepts to Master
- **User Mode vs. Kernel Mode:** High security (safe) vs. High privilege (dangerous).
- **The Mode Switch:** The CPU transition that happens when a syscall is triggered.
- **The Syscall Table:** A numbered list of functions the kernel provides (e.g., #0 is `read`, #1 is `write`).
- **Strace / Dtruss:** Tools for watching every syscall an application makes in real-time.

### Research Topics
- "What is a system call?"
- "The steps of a syscall: From library to trap"
- "List of Linux syscalls (packages.ubuntu.com/syscalls)"
- "Performance overhead of context switching during a syscall"

---

### The Practical Challenge

**Part 1: The `Strace` Adventure (Linux/Mac)**
1. On Linux: `strace ls`.
2. On Mac: `sudo dtruss ls`.
3. Observe the output. Identify calls like `open`, `read`, `mmap`, and `write`.
4. Discuss: Your `ls` command didn't just "print text"—it asked the kernel to `write(1, "myfile\n", 7)`.

**Part 2: The mode switch penalty**
1. Read a 1GB file in two ways:
   - Method A: read 1 byte at a time (calls 1,000,000,000 syscalls).
   - Method B: read 1MB at a time (calls 1,000 syscalls).
2. Measure the time difference. 
3. Discuss: Why does the "Boundary Crossing" make Method A so slow?

**Part 3: The Write Syscall (C/Assembly)**
1. Research the C `write()` function. 
2. Identify the arguments: File Descriptor, Pointer to Data, Length.
3. Discuss: Why can the Kernel see your pointer, but you can't see the Kernel's internal buffers?

**Part 4: Identifying Privileged Actions**
1. List 5 things a program *cannot* do without a syscall:
   - (Answer: Access hardware, Talk to net, Delete a file it doesn't own, Shut down PC, Allocate more RAM).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Security Vulnerabilities. Syscalls are the primary attack surface for hackers. If a syscall like `ptrace` is poorly guarded, a user can "become" the root user.
- **Gotcha 2:** OS Portability. A syscall number on Linux (#60 for `exit`) is different than on Mac or Windows. This is why we use "Libraries" (libc) to hide the raw numbers.

### Reflection Question
Why are syscalls much slower than regular "Function Calls" inside your program? (Answer: mode switching, register saving, and privilege validation).
