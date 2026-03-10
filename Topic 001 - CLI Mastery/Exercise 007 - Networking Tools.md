# Exercise 007 - Networking for Developers (CLI Tools)

### Objective
Diagnose connectivity issues from the command line. Master the native networking utilities (`ping`, `curl`, `netstat`, `dig`) required to troubleshoot DNS failures, network latency, and server availability.

### Core Concepts to Master
- **IP & DNS Resolution:** Understanding how the computer translates a URL (`google.com`) into an IP address using `dig` or `nslookup`.
- **Latency & Reachability:** Using `ping` to measure round-trip time and `traceroute` to see the "hops" your data takes across the internet.
- **Port Checking:** Using `nc` (Netcat) or `telnet` to see if a specific port (e.g., 80, 443, 3000) is open on a remote server.
- **Header Inspection:** Using `curl -I` to view HTTP response headers without downloading the entire body.

### Research Topics
- "Basic network troubleshooting commands for developers"
- "How to use curl to test an API"
- "Understanding DNS records (A, CNAME, TXT)"
- "Whst is traceroute and how to read it"

---

### The Practical Challenge

**Part 1: Basic Reachability**
1. Ping a global server: `ping google.com`. Observe the `time=...ms` values.
2. Ping a server on a different continent (e.g., `ping bbc.co.uk` from the US). Compare the latency.
3. Run `traceroute google.com`. Observe how many "Hops" (routers) your request passes through before reaching the destination.

**Part 2: DNS Digging**
1. Use `dig google.com` to find the "A" record (The IP address).
2. Use `nslookup` as an alternative.
3. Use `dig +short google.com` to get only the IP.
4. Research what a "TTL" (Time To Live) value means in a DNS response.

**Part 3: Testing App Ports**
1. Stat a local web server (e.g., `npx serve` or a Node.js app) on port 3000.
2. Verify it is listening using `lsof -i :3000` or `netstat -an | grep 3000`.
3. Use `nc -vz localhost 3000` to "Scan" the port and confirm it is open. 
4. Try to scan a port that isn't open (e.g., 3001) and observe the "Connection Refused" error.

**Part 4: Curl for API Testing**
1. Use `curl` to fetch a public API: `curl https://jsonplaceholder.typicode.com/posts/1`.
2. Inspect only the headers: `curl -I https://google.com`.
3. Practice sending a `POST` request with a JSON body using `curl -X POST -H "Content-Type: application/json" -d '{"title": "foo"}'`.
4. Discuss why `curl` is often faster for testing simple API endpoints than opening a full GUI like Postman.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Firewall Blocks. Some servers block `ping` (ICMP) for security reasons. Just because a server doesn't respond to a ping doesn't mean it's down.
- **Gotcha 2:** Local vs Public IPs. Your computer has a local IP (e.g., `192.168.x.x`) and a public IP. `ipconfig` or `ifconfig` shows the local one, while `curl ifconfig.me` shows the public one.

### Reflection Question
Why is `curl` considered the "Swiss Army Knife" of network and API development?
