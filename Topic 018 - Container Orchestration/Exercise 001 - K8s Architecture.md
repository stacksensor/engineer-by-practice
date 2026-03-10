# Exercise 001 - K8s Architecture & Control Plane

### Objective
Understand the brain of the cluster. Explore the core components of the Kubernetes Control Plane and worker nodes, learning how the API Server, Scheduler, and ETCD work together to maintain the desired state of your applications.

### Core Concepts to Master
- **Control Plane:** The collection of components (API Server, ETCD, Scheduler, Controller Manager) that manage the cluster.
- **Worker Nodes:** The machines where your applications actually run (containing Kubelet and Kube-proxy).
- **The API Server:** The central hub that all components talk to. It is the only component that interacts directly with ETCD.
- **ETCD:** A distributed key-value store that acts as the cluster's single source of truth.

### Research Topics
- "Kubernetes architecture diagram explained"
- "What is the role of the Kubelet?"
- "ETCD vs traditional databases in K8s"
- "Installing minikube or kind for local testing"

---

### The Practical Challenge

**Part 1: Setting up the Lab**
1. Install a local Kubernetes cluster using `minikube` or `kind`.
2. Verify the cluster is running: `kubectl cluster-info`.
3. List the nodes in your cluster: `kubectl get nodes`.

**Part 2: Exploring the Control Plane**
1. Most local clusters run control plane components as Pods in the `kube-system` namespace.
2. List all pods in that namespace: `kubectl get pods -n kube-system`.
3. Identify the pods for `kube-apiserver`, `etcd`, and `kube-scheduler`.
4. Use `kubectl describe pod <apiserver-pod-name> -n kube-system` to see the configuration flags used to start the API server.

**Part 3: Simulated Failure**
1. Discuss: What happens to your running applications if the `kube-scheduler` pod is deleted or stopped?
2. Experiment: Intentionally delete a non-critical control plane pod (if your local setup allows) and observe how the system automatically recreates it.

**Part 4: Interaction Flow**
1. Path of a Request: When you run `kubectl apply -f pod.yaml`, trace the journey of that request through the control plane components.
2. Sketch a diagram showing the interaction between the User, API Server, ETCD, and the Kubelet on a worker node.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Context Mismatch. If you have multiple clusters, `kubectl` might be talking to the wrong one. Always check your current context with `kubectl config current-context`.
- **Gotcha 2:** ETCD Corruption. In production, ETCD is the most critical component. If you lose your ETCD data without a backup, your cluster is essentially gone.

### Reflection Question
Why is the API Server the only component allowed to talk to ETCD, and how does this design contribute to cluster security and consistency?
