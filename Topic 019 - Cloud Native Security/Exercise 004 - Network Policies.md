# Exercise 004 - Network Policies

### Objective
Implement "Zero Trust" networking. By default, every pod in a Kubernetes cluster can talk to every other pod. Learn how to use **NetworkPolicies** to act as a distributed firewall, restricting traffic so that only specific services can communicate with each other.

### Core Concepts to Master
- **Ingress vs. Egress:** Controlling traffic coming *into* a pod (Ingress) vs traffic going *out* of a pod (Egress).
- **Selectors (Pod/Namespace):** Defining traffic rules based on labels rather than IP addresses.
- **Protocol & Port:** Specifically allowing traffic on certain ports (e.g., 5432 for Postgres) while blocking everything else.
- **Deny-All Default:** Creating a policy that blocks everything by default and only explicitly whitelisting what is needed.

### Research Topics
- "Do all CNI plugins support NetworkPolicies?"
- "Kubernetes NetworkPolicy tutorial"
- "Testing network policies with 'exec curl'"

---

### The Practical Challenge

**Part 1: The Default Vulnerability**
1. Create two namespaces: `frontend-ns` and `database-ns`.
2. Deploy an `nginx` pod in `database-ns`.
3. Deploy a `curl` pod in `frontend-ns`.
4. Verify that the `curl` pod can reach the `nginx` pod across namespaces.
5. Discuss: Why is this undesirable in a secure production environment?

**Part 2: Deny All Default**
1. Apply a "Deny-All" NetworkPolicy to the `database-ns`.
2. Try the `curl` again from `frontend-ns`. It should now hang or time out.
3. Observe that even pods *inside* `database-ns` can no longer talk to each other.

**Part 3: The Targeted Whitelist**
1. Create a new NetworkPolicy in `database-ns` named `allow-frontend-to-db`.
2. Configure the `ingress` rule to allow traffic only if:
   - The namespace has the label `name: frontend-ns`.
   - The pod has the label `role: frontend`.
   - The port is `80`.
3. Re-test. The `curl` should now work, but only from pods matching those specific labels.

**Part 4: Egress Lockdown**
1. Research how to block "Egress" traffic. 
2. Create a policy that prevents your database pods from reaching out to the public internet (useful for preventing "Data Exfiltration" if a database is compromised).
3. Test by trying to `curl google.com` from inside your database pod.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** CNI Requirement. NetworkPolicies are just "declarations." You need a CNI (Container Network Interface) plugin like **Calico**, **Cilium**, or **Antrea** to actually enforce them. Standard `minikube` or `kind` with default networking might ignore your policies entirely!
- **Gotcha 2:** Cumulative Rules. If multiple NetworkPolicies apply to a pod, the result is the "Union" of all rules. If one policy denies everything but another allows port 80, port 80 will be open.

### Reflection Question
How does "Namespace isolation" differ from "NetworkPolicy isolation," and why should you use both?
