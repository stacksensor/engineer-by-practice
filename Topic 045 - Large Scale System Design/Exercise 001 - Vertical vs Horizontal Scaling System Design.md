# Exercise 001 - Vertical vs. Horizontal Scaling (System Design)

### Objective
Scale for millions. Master the two most important strategies for handling increasing user demand: **Vertical Scaling** (Buying a "Bigger" computer) and **Horizontal Scaling** (Buying "More" computers). Learn the hard limits of hardware and why "State" (like a session or a database) is the enemy of horizontal scaling.

### Core Concepts to Master
- **Vertical Scaling (Scaling Up):** Upgrading your single server to have 128 cores and 1TB of RAM. (Easy, but expensive and hits a hardware "Ceiling").
- **Horizontal Scaling (Scaling Out):** Adding 50 cheap servers in a cluster. (Infinite, but requires a Load Balancer and "Stateless" code).
- **The Load Balancer:** The "Front Door" that decides which of your 50 servers gets the current user's request.
- **The Stateless Rule:** A user's request must be processable by ANY of the 50 servers. (No data should be saved only in the local memory of one server).

### Research Topics
- "Vertical vs Horizontal Scaling: The ultimate trade-offs"
- "Why horizontal scaling is better for high availability"
- "What happens when you hit the 'Hardware Ceiling' for vertical scaling?"
- "The cost of managing 1,000 small servers vs 1 big server"

---

### The Practical Challenge

**Part 1: The "State" Disaster**
1. You have 2 Servers: A and B. A Load Balancer is in front.
2. User Alex logs in. The Load Balancer sends them to Server A.
3. Server A saves `loggedIn: true` in its own RAM.
4. Alex refreshes the page. The Load Balancer sends them to Server B.
5. Discuss: Does Server B know Alex is logged in? 
6. (Answer: No! Alex is suddenly "Logged out").

**Part 2: The "Stateless" Fix**
1. Research how to solve this using a "Shared Store":
   - **Database / Redis:** Both servers check one central Redis to find the login.
   - **JWT:** The login is stored in a cookie in the user's browser, not on the server.
2. Discuss why this makes scaling out "Infinite."

**Part 3: The Price of Scale**
1. Research the cost of a **64-core 256GB RAM** server in AWS (e.g., `x2gd.4xlarge`).
2. Research the cost of **16 x 4-core 16GB RAM** servers.
3. Discuss: Which one is cheaper for the same "Total CPU/RAM"? (Answer: Usually the smaller ones are much cheaper).

**Part 4: Identifying the strategy**
1. Which scaling strategy for:
   - "A single-player game you run once a month for 1 hour" (Answer: Vertical).
   - "A globally distributed social network with 100 million users" (Answer: Horizontal).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Deadlock on the Load Balancer. If your Load Balancer is not "Highly Available," it becomes a "Single Point of Failure" for your entire 50-server cluster.
- **Gotcha 2:** The "Sticky Session" trap. Some Load Balancers allow "Sticky Sessions" (forcing a user to stay on Server A). Discuss why this makes "Scaling Down" (deleting Server A) very dangerous for that user.

### Reflection Question
Why is Horizontal Scaling considered the "Foundation" of modern cloud computing (like AWS/GCP/Azure)? (Answer: Because the cloud is built on thousands of cheap, replaceable servers rather than one giant supercomputer).
