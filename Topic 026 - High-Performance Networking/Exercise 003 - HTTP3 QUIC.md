# Exercise 003 - HTTP/3 & QUIC

### Objective
Understand the future of the web. Learn about **HTTP/3** and the underlying **QUIC** protocol (Quick UDP Internet Connections). Explore how moving from TCP to UDP eliminates "Head-of-Line Blocking" and how 0-RTT handshakes significantly reduce latency for users on mobile or unreliable networks.

### Core Concepts to Master
- **TCP Head-of-Line Blocking:** Why a single dropped packet in TCP stops *all* data streams in an HTTP/2 connection.
- **QUIC (UDP-based):** How QUIC handles packet loss and congestion control at the application layer instead of the OS kernel.
- **Connection Migration:** How a user can switch from Wi-Fi to a 4G/5G data network without their active HTTP/3 connection breaking.
- **0-RTT (Zero Round Trip Time):** Allowing a client to send data (encrypted) in their very first packet to the server if they have connected before.

### Research Topics
- "What is QUIC and why did Google build it?"
- "HTTP/1 vs HTTP/2 vs HTTP/3 visual comparison"
- "Troubleshooting UDP port 443 for HTTP/3"

---

### The Practical Challenge

**Part 1: The TCP vs. UDP Mindset**
1. Research the difference between TCP (Reliable/Connection-oriented) and UDP (Unreliable/Connectionless).
2. Discuss: Why was UDP traditionally considered "bad" for web traffic, and how does QUIC make it "reliable" again?

**Part 2: Head-of-Line Blocking (Conceptual)**
1. Imagine an HTTP/2 connection downloading 3 images. 
2. If packet #5 for Image A is lost, the browser cannot read packets #6 onwards for *any* of the images until #5 is re-sent.
3. Draw a diagram showing how HTTP/3 (QUIC) handles this by treating each image as an independent stream.

**Part 3: Testing for HTTP/3**
1. Open Chrome or Firefox DevTools. 
2. Go to a site like `google.com` or `facebook.com`.
3. Look at the "Protocol" column in the Network tab. 
4. Identify requests using `h3`. Discuss why not every site uses it yet.

**Part 4: Mobile Handover (Conceptual)**
1. Research "QUIC Connection IDs."
2. Explain how a Connection ID allows a server to recognize a user even if their IP address changes (e.g., walking out of your house and switching from Home Wi-Fi to 5G).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Firewall Blocks. Many corporate firewalls block outbound UDP traffic on port 443 by default because it looks like a potential attack. Most browsers will "Fallback" to HTTP/2 in this case.
- **Gotcha 2:** CPU Cost. Because QUIC handles encryption and congestion control in "User Space" rather than the Kernel, it can sometimes be more CPU-intensive for high-traffic servers than TCP.

### Reflection Question
How does 0-RTT help improve the "Perceived Load Time" for a user who frequently visits your website?
