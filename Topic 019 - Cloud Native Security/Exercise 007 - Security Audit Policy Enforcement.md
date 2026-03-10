# Exercise 007 - Security Audit & Policy Enforcement (Kyverno)

### Objective
Automate your security governance. Move from "Guidelines" to "Enforced Policies." Learn how to use **Kyverno** (a Kubernetes-native policy engine) to automatically audit and block any resource that doesn't follow your security standards (e.g., denying images that run as root or requiring specific labels).

### Core Concepts to Master
- **Policy Engine:** A tool that validates or mutates K8s resources before they are saved to ETCD.
- **Admission Controller:** The K8s hook that triggers the policy engine.
- **Validate Rules:** Policies that "Audit" (allow but warn) or "Enforce" (block) resources.
- **Mutate Rules:** Policies that automatically "Fix" resources (e.g., adding a default resource limit if one is missing).

### Research Topics
- "Kyverno vs OPA Gatekeeper"
- "How to write Kyverno policies without learning a new language"
- "Kyverno admission controller hooks"

---

### The Practical Challenge

**Part 1: Installing the Guardian**
1. Install Kyverno into your cluster using Helm.
2. Verify the pods are running in the `kyverno` namespace.

**Part 2: The "No Root" Policy**
1. Create a `ClusterPolicy` that validates all pods.
2. Set the rule to check if `securityContext.runAsNonRoot` is `true`.
3. Set the `validationFailureAction` to `Audit`.
4. Apply the policy.
5. Deploy a pod that runs as root. Check the Kyverno logs or the `PolicyReport` object. It should show a "Warning" but allow the pod to run.

**Part 3: Moving to Enforce**
1. Change the policy's `validationFailureAction` to `Enforce`.
2. Try to deploy the root pod again.
3. Observe that the K8s API Server now blocks the request: `Error from server: admission webhook ... denied the request`.

**Part 4: Auto-Mutating Resource Limits**
1. Create a "Mutate" policy. 
2. If a developer creates a deployment without `resources.limits.cpu`, Kyverno should automatically add a default limit of `500m`.
3. Test by applying a minimal deployment.
4. Run `kubectl get pod <name> -o yaml` and notice that the limits are magically present!

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Mutating the Cluster. If you write a buggy Mutate policy, it can break the entire cluster by making every new pod invalid. Always test policies in a local environment first.
- **Gotcha 2:** Excluding Namespaces. Some policies might break system-level pods (like those in `kube-system`). Always include `exclude` rules for critical system namespaces.

### Reflection Question
How does moving security enforcement to a "Policy Engine" help reduce the burden on your Security Review Team?
