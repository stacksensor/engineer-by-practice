# Exercise 002 - RBAC (Role-Based Access Control)

### Objective
Enforce the "Principle of Least Privilege." Learn how to use Kubernetes Role-Based Access Control (RBAC) to define exactly who (users or bots) can do what (get, list, delete) to which resources (pods, services, secrets) in your cluster.

### Core Concepts to Master
- **ServiceAccount:** An identity for processes running in your pods.
- **Role / ClusterRole:** A set of permissions (Rules) that describe available actions.
- **RoleBinding / ClusterRoleBinding:** The "Glue" that grants the permissions in a Role to a specific ServiceAccount or User.
- **Namespacing:** Roles are restricted to a single namespace, while ClusterRoles apply to the entire cluster.

### Research Topics
- "Kubernetes RBAC api groups and verbs"
- "Difference between Role and ClusterRole"
- "How to test RBAC with 'kubectl auth can-i'"

---

### The Practical Challenge

**Part 1: The "Restricted" Identity**
1. Create a namespace named `secure-app`.
2. Create a ServiceAccount named `pod-reader` in that namespace.
3. Verify it: `kubectl get sa pod-reader -n secure-app`.

**Part 2: Defining the Permission**
1. Create a Role named `read-pods`.
2. Add rules that allow `get`, `list`, and `watch` for the resource `pods`.
3. Do NOT allow `delete` or `create`.

**Part 3: Binding the Identity**
1. Create a RoleBinding that links the `read-pods` Role to the `pod-reader` ServiceAccount.
2. Apply it.
3. Test the permission: `kubectl auth can-i get pods --as=system:serviceaccount:secure-app:pod-reader -n secure-app`. (Result: `yes`).
4. Test a forbidden action: `kubectl auth can-i delete pods --as=system:serviceaccount:secure-app:pod-reader -n secure-app`. (Result: `no`).

**Part 4: Cluster-Wide Permissions**
1. Create a ClusterRole that allows viewing nodes: `kubectl create clusterrole node-viewer --verb=get,list --resource=nodes`.
2. Bind it to your ServiceAccount across the entire cluster using a ClusterRoleBinding.
3. Verify the bot can now see global infrastructure but still cannot delete pods in its own namespace.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The Default ServiceAccount. Every namespace has a `default` SA. If you don't explicitly assign a ServiceAccount to a pod, it uses the default one, which often has too many (or too few) permissions.
- **Gotcha 2:** Verb Overload. Use caution with verbs like `use`, `impersonate`, or `proxy`, as these can lead to privilege escalation attacks.

### Reflection Question
Why is giving every developer "ClusterAdmin" access a major security risk for a multi-tenant production cluster?
