# Exercise 001 - Networking Layers (OSI Model)

### Objective
Deconstruct the theoretical architecture of the internet. Master the OSI (Open Systems Interconnection) model to understand exactly how physical electrical signals are converted into high-level browser applications.

### Core Concepts to Master
- **The OSI 7-Layer Model:** The conceptual framework used to describe the functions of a networking system.
- **Physical to Application:** The journey of data from raw 1s and 0s over copper wire (Layer 1) to a fully rendered webpage (Layer 7).
- **Encapsulation:** How each layer wraps the payload with specific metadata headers before passing it down the stack.
- **TCP/IP Model:** The practical, condensed 4-layer model that the modern internet actually runs on.

### Research Topics
- "OSI vs TCP/IP models explained"
- "Data encapsulation networking"
- "What happens when you type google.com"

---

### The Practical Challenge

**Part 1: The Physical and Data Link Layers**
1. Open your terminal.
2. We are going to inspect the hardware layer. Run `arp -a` (Windows/Mac).
3. Review the output. You will see IP addresses mapped directly to MAC (Media Access Control) addresses.
4. The MAC address is the physical hardware identifier hardcoded into the silicon of your device's network card. This operates at Layer 2 (Data Link).

**Part 2: The Network Layer (IP)**
1. Layer 3 is responsible for routing data across massive geographical networks using IP Addresses.
2. In your terminal, run `traceroute google.com` (Mac/Linux) or `tracert google.com` (Windows).
3. Watch the output mathematically jump ("hop") across 10 to 15 different physical routers globally. 
4. Each line represents a distinct physical server intercepting your packet, reading the destination IP in the Layer 3 header, and throwing it to the next closest node.

**Part 3: The Transport Layer (TCP vs UDP)**
1. Layer 4 handles defining how the data is sent.
2. TCP (Transmission Control Protocol) is slow but perfectly reliable. It requires a "Three-Way Handshake" to establish a secure connection, heavily verifying every single byte of data.
3. UDP (User Datagram Protocol) is incredibly fast but unreliable. It blindly blasts data packets without checking if they were received.
4. Use standard network tools (like Wireshark if installed, or specific browser dev tools) to analyze the handshake process of a standard website connection.

**Part 4: The Application Layer**
1. Layer 7 is where developers spend 99% of their time (HTTP, FTP, SSH).
2. Open your browser's Developer Tools network tab.
3. Enter a URL and observe the raw HTTP headers. 
4. This visible high-level text data is the ultimate payload that the 6 previous layers successfully encapsulated, routed, and decrypted.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Junior developers often confuse switch routing (Layer 2 MAC hardware level) with IP routing (Layer 3 software logic level). Local networks rely entirely on MAC addresses. The global internet relies on IP addresses.
- **Gotcha 2:** Implementing TCP for real-time video games creates massive jitter due to packet verification checks. Implementing UDP for a financial banking system results in catastrophic lost transactions. Use the correct Transport algorithm for the software architecture.

### Reflection Question
Why is the strict 7-layer OSI model primarily referenced in academia and architectural diagrams, whereas the modern internet physically operates exclusively on the 4-layer TCP/IP suite?