# Exercise 002 - Virtualization & Hypervisors

### Objective
Understand the separation of hardware and software. Explore the history and utility of Virtual Machines (VMs) and Hypervisors, laying the conceptual groundwork for modern containerization and cloud infrastructure.

### Core Concepts to Master
- **Virtualization:** The process of running multiple, isolated operating systems simultaneously on a single physical "Host" machine.
- **Hypervisor:** The specialized software layer (e.g., VirtualBox, VMWare, KVM) that manages and distributes physical CPU/RAM resources to virtual instances.
- **Snapshotting:** The ability to save the exact state of a virtual OS and "roll back" instantly to that moment in time if something breaks.
- **Hardware Isolation:** Ensuring that a crash or security breach in one Virtual Machine cannot propagate to the Host or other neighboring VMs.

### Research Topics
- "Difference between Type 1 and Type 2 Hypervisors"
- "How virtualization changed the server industry"
- "VMware vs VirtualBox vs Proxmox"

---

### The Practical Challenge

**Part 1: Identifying the Hypervisor**
1. Research the hypervisor currently running on your machine (e.g., macOS uses Hyper Kit/Virtualization Framework, Windows uses Hyper-V).
2. Download or use a pre-installed virtualization tool (like VirtualBox or VMware Player).
3. Attempt to create a "New" machine. Notice the hardware allocation settings (CPU cores, RAM size, Disk space).

**Part 2: ISO Bootstrapping**
1. Download a "Server" ISO file (e.g., Ubuntu Server 22.04).
2. Attach this ISO to your virtual machine's virtual optical drive.
3. Boot the machine. Observe how the virtual BIOS/UEFI starts and begins the installation process within a window on your desktop.

**Part 3: The Virtual Interface**
1. Understand Virtual Networking.
2. Explore the difference between "NAT" (where the VM shares the host's IP) and "Bridged" (where the VM appears as a separate device on your physical home/office router).
3. Try to `ping` your Host machine FROM the VM once it's finished installing.

**Part 4: The Snapshost Safety Net**
1. Install a specific software package in your VM (e.g., `sudo apt install nginx`).
2. Create a "Snapshot" named "Web Server Installed".
3. Intentionally break the OS (e.g., delete a core system folder or mess up the network config).
4. Use the "Restore" function to revert to your snapshot. Notice how the machine is perfectly restored to its functional state in seconds.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Nested Virtualization. Running a VM inside another VM is extremely difficult and often requires specific hardware flags to be enabled in the Host BIOS (VT-x or AMD-V).
- **Gotcha 2:** Resource Exhaustion. If you assign 10GB of RAM to a VM on a machine that has 16GB total, your Host OS will likely freeze or lag significantly. Always leave enough overhead for the Host machine to breathe.

### Reflection Question
If Virtual Machines provide perfect isolation, why is the industry moving toward Docker "Containers" which share the same underlying Linux kernel?