# Exercise 004 - Service Mesh (Istio & Envoy)

### Objective
Manage the network between your services. Master the **Service Mesh** pattern. Learn how to use **Istio** and the **Envoy proxy** to handle "Plumbing" tasks like mutual TLS (mTLS), retries, timeouts, and traffic splitting without writing a single line of networking code in your application.

### Core Concepts to Master
- **The "Sidecar" Proxy:** Moving networking logic out of the app and into a separate container (Envoy) that sits next to it.
- **Control Plane vs. Data Plane:** 
  - **Data Plane:** The proxies (Envoy) that handle the actual traffic.
  - **Control Plane:** The system (Istio) that manage the proxies.
- **Mutual TLS (mTLS):** Automatically encrypting all traffic between your microservices with identity-based certificates.
- **Ingress & Egress Gateways:** Controlling how traffic enters and leaves your cluster.

### Research Topics
- "What is a Service Mesh and why do I need one?"
- "The Envoy Proxy architecture"
- "Istio: Traffic management features (VirtualServices, DestinationRules)"

---

### The Practical Challenge

**Part 1: The Sidecar Injection**
1. Install Istio into a local Kubernetes cluster.
2. Label a namespace for "Sidecar Injection": `kubectl label namespace default istio-injection=enabled`.
3. Deploy a simple app. 
4. Run `kubectl get pods`. Notice that the "READY" column now shows `2/2` (Your app + the Envoy proxy).

**Part 2: mTLS Verification**
1. By default, Istio tries to upgrade all traffic to mTLS.
2. Use a tool like `tcpdump` inside one of your pods to inspect traffic from another pod.
3. Verify that the traffic is encrypted and unreadable as plain text.

**Part 3: Canary Deployments (Traffic Splitting)**
1. Deploy two versions of an app (`v1` and `v2`).
2. Create an Istio **VirtualService** that sends 90% of traffic to `v1` and 10% to `v2`.
3. Test by running a loop of requests and observing the distribution.

**Part 4: The Fault Injection**
1. Use Istio to intentionally delay traffic to a specific service by 5 seconds (to test your app's timeout logic).
2. Configure a "Retry Policy" that automatically retries a failed request 3 times before returning an error to the user.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Complexity Overhead. A Service Mesh adds a massive amount of complexity to your cluster. If you only have 3-5 microservices, you almost certainly don't need one.
- **Gotcha 2:** Latency Tax. Every request now has to travel through two extra proxies (Client-proxy -> Server-proxy). This usually adds 1-2ms of latency.

### Reflection Question
How does a Service Mesh allow a company with 100 microservices to enforce a "Zero Trust" security policy across all of them at once?
