# Exercise 002 - Pods & ReplicaSets

### Objective
Master the atomic unit of Kubernetes. Learn how to define, deploy, and manage Pods, and use ReplicaSets to ensure that a specific number of pod replicas are running at all times, providing basic self-healing capabilities.

### Core Concepts to Master
- **The Pod:** The smallest deployable unit in K8s, consisting of one or more containers that share network and storage.
- **YAML Manifests:** The declarative files used to describe the desired state of K8s objects.
- **ReplicaSet:** A controller that ensures a stable set of replica Pods are running at any given time.
- **Labels & Selectors:** The "Identity" system K8s uses to link controllers (ReplicaSets) to the Pods they manage.

### Research Topics
- "Kubernetes Pod lifecycle (Pending, Running, Succeeded, Failed)"
- "Label selectors in Kubernetes"
- "Difference between a Pod and a Container"

---

### The Practical Challenge

**Part 1: The Simple Pod**
1. Create a file named `nginx-pod.yaml`.
2. Define a Pod using the `nginx:latest` image.
3. Apply it: `kubectl apply -f nginx-pod.yaml`.
4. Check the status: `kubectl get pods`. Wait until it is in the `Running` state.
5. Access the logs: `kubectl logs nginx-pod`.

**Part 2: Multi-Container Pods (Sidecars)**
1. Update your YAML to include a second "Sidecar" container (e.g., a simple `busybox` container that sleeps).
2. Apply the change. Notice that `kubectl get pods` now shows `2/2` containers ready.
3. Access a shell inside the sidecar: `kubectl exec -it nginx-pod -c busybox-container -- sh`.

**Part 3: The ReplicaSet**
1. Create a `nginx-rs.yaml` file.
2. Define a ReplicaSet with `spec.replicas: 3`. 
3. Ensure the `selector` matches the `labels` in the pod template.
4. Apply the ReplicaSet and verify 3 pods are created: `kubectl get pods`.

**Part 4: Self-Healing in Action**
1. Manually delete one of the 3 pods created by the ReplicaSet: `kubectl delete pod <pod-name>`.
2. Immediately run `kubectl get pods`.
3. Watch as the ReplicaSet notices the "Current State" (2 pods) does not match the "Desired State" (3 pods) and automatically spawns a new one.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Immutable Fields. Some fields in a Pod manifest (like the container name) cannot be changed after the Pod is created. You must delete and recreate the Pod.
- **Gotcha 2:** ImagePullBackOff. If you typo the image name (e.g., `nginxx`), the pod will enter an error loop. Use `kubectl describe pod <name>` to see the specific error event.

### Reflection Question
If Pods are ephemeral (they can die and be replaced at any time), why is it considered a "Bad Practice" to manually create individual Pods instead of using a Controller like a ReplicaSet or Deployment?
