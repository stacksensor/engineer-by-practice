# Exercise 004 - Network Performance: TCP vs. UDP & HTTP/3

### Objective
Master the wire. Master **Network Performance**—the most common "Invisible" bottleneck in modern apps. Learn the difference between **TCP** (Reliable, but slow due to Handshakes) and **UDP** (Fast, but lossy). Understand why **HTTP/2** and **HTTP/3 (QUIC)** were invented to solve the "Head-of-Line Blocking" problem.

### Core Concepts to Master
- **TCP (Transmission Control Protocol):** The "Phone Call" (Handshake, Data, Finish). Guarantees every byte arrives.
- **UDP (User Datagram Protocol):** The "Radio Broadcast" (Send and hope for the best). No handshake. Fast.
- **Round-Trip Time (RTT):** The time for a packet to go to the server AND back. (e.g., 20ms).
- **The "Three-Way Handshake":** Synthesize the 1.5 RTT delay before you can even send a single character of data.
- **HTTP/2 Multiplexing:** Sending 50 images over ONE TCP connection instead of 50 separate slow connections.
- **Head-of-Line Blocking:** One slow image blocking the other 49 from loading.
- **HTTP/3 (QUIC):** Moving HTTP onto **UDP** to eliminate the final "Blocking" bugs.

### Research Topics
- "TCP Handshake vs HTTP Handshake"
- "HTTP/1.1 vs HTTP/2 vs HTTP/3: Key differences"
- "Why does a 1% packet loss kill TCP more than UDP?"
- "The concept of '0-RTT' in HTTP/3"

---

### The Practical Challenge

**Part 1: The TCP Handshake (Conceptual)**
1. You want to ask: "Hi?". 
2. In TCP, you have to do:
   - "Client: SYN" (Wait 1 RTT).
   - "Server: SYN-ACK" (Wait 0.5 RTT).
   - "Client: ACK + Data" (Wait 0.5 RTT).
3. If your RTT is 100ms, how long until the server sees your 1-byte "Hi"? 
4. (Answer: 200ms - 2 full round trips!).

**Part 2: The "Loss" Penalty**
1. Research what happens in **TCP** when 1 packet out of 100 is lost. 
2. (Answer: TCP stops EVERYTHING, waits to detect the loss, and re-sends the packet. This cause a "Freeze" in your app).
3. Discuss why **UDP** is better for "Zoom calls" or "Gaming" because you can just "Skip" the lost frame.

**Part 3: HTTP/2 in Chrome**
1. Open Chrome DevTools -> Network. 
2. Right-click the columns and check **"Protocol."**
3. Refresh a site like Google or Facebook. 
4. See `h2` or `h3` in the list.
5. Discuss: Why does your "Logo" and "Profile Picture" load at the same time instead of one-by-one?

**Part 4: Identifying the protocol**
1. Which one for:
   - "A financial trade" (Answer: TCP).
   - "A real-time multiplayer FPS game" (Answer: UDP).
   - "A voice-over-IP call" (Answer: UDP).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** MTU (Maximum Transmission Unit). If you try to send a packet larger than 1,500 bytes, the router might "Fragment" it into 2 pieces, doubling your latency.
- **Gotcha 2:** Only measuring "Bandwidth" (e.g., 'I have 1Gbps!'). For apps, **Latency** (RTT) is usually much more important than raw speed.

### Reflection Question
Why did the internet move from TCP-based HTTP/2 to UDP-based HTTP/3 in 2022? (Answer: To eliminate the "Head-of-Line" congestion that happened whenever a single Wi-Fi packet was lost).
