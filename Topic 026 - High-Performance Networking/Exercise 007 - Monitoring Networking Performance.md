# Exercise 007 - Monitoring Networking Performance

### Objective
Measure the pipe. Learn how to identify and debug network bottlenecks using tools like **Ping**, **Traceroute**, **MTR**, and **Wireshark**. Understand concepts like **Throughput** vs. **Latency**, and how **Jitter** and **Packet Loss** affect real-time applications like VoIP and gaming.

### Core Concepts to Master
- **Round-Trip Time (RTT):** The time it takes for a packet to reach the destination and come back.
- **Bandwidth/Throughput:** How much data can fit in the pipe (e.g., 100Mbps).
- **Packet Loss:** What % of data never arrives.
- **Jitter:** The variation in latency (e.g., if one packet takes 10ms and the next takes 500ms, the audio in a Zoom call will stutter).
- **Bufferbloat:** When routers "Buffer" too much data, causing latency to skyrocket.

### Research Topics
- "What is MTR and how to read its report?"
- "Basics of packet analysis with Wireshark"
- "Troubleshooting high latency: Is it the server or the network?"

---

### The Practical Challenge

**Part 1: The Path Tracer**
1. Run `traceroute google.com` (or `tracert` on Windows).
2. Observe every "Hop" (router) your packet passes through. 
3. Locate where the packet leaves your ISP and enters the backbone network.

**Part 2: MTR (Path Performance)**
1. Install **MTR** (My Traceroute).
2. Run `mtr google.com`. Keep it running for 60 seconds.
3. Observe the "Loss %" and "Avg" latency for every hop. 
4. If hop #3 shows 50% loss but hop #4 shows 0% loss, is there actually a problem with the network? (Hint: Some routers rate-limit TTL-expired packets).

**Part 3: Packet Sniffing (Wireshark/tcpdump)**
1. Research how to use `tcpdump` on a specific port: `tcpdump -i eth0 port 80`.
2. (Conceptual or Lab): Capture an HTTP request. 
3. Identify the "SYN," "SYN-ACK," and "ACK" packets of the TCP handshake.

**Part 4: Simulating Bad Connections**
1. Research tools like `tc` (Traffic Control) on Linux. 
2. Learn how to intentionally add 500ms of latency or 5% packet loss to your local network interface to see how your application handles it.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Measuring the wrong thing. High CPU on a server can look like a "Network Problem" because the server takes too long to process a packet. Check server health before blaming the ISP.
- **Gotcha 2:** ICMP Blocking. Many high-security servers (and some ISPs) block `ping` and `traceroute` packets entirely to hide their infrastructure. A "Timed Out" response doesn't always mean the server is down.

### Reflection Question
Why is "Low Latency" more important than "High Bandwidth" for an online competitive First-Person Shooter game?
