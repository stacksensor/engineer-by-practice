# Exercise 005 - Persistent Volumes & Storage

### Objective
Provide state to your stateless cluster. Learn how to use **Persistent Volumes (PV)** and **Persistent Volume Claims (PVC)** to allow database and stateful application data to survive pod restarts or node failures.

### Core Concepts to Master
- **Persistent Volume (PV):** A piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes.
- **Persistent Volume Claim (PVC):** A request for storage by a user (Pod). It specifies the size and access modes needed.
- **Access Modes:** `ReadWriteOnce` (RWO), `ReadOnlyMany` (ROX), and `ReadWriteMany` (RWX).
- **Storage Class:** A way for administrators to describe the "classes" of storage they offer (e.g., "fast-ssd", "slow-hdd").

### Research Topics
- "Static vs Dynamic provisioning in Kubernetes"
- "How do PVCs bind to PVs?"
- "Reclaim policies: Delete vs Retain"

---

### The Practical Challenge

**Part 1: The Local Claim**
1. Check available storage classes in your cluster: `kubectl get storageclass`.
2. Create a `data-pvc.yaml` file.
3. Request 1Gi of storage with the `ReadWriteOnce` access mode.
4. Apply the PVC and check its status: `kubectl get pvc`. It might stay in `Pending` until a pod uses it (depending on the storage class).

**Part 2: Attaching to a Pod**
1. Create a Pod that uses the `data-pvc` as a volume mounted at `/data`.
2. Apply the pod. Verify that the PVC status is now `Bound`.
3. Exec into the pod and write a file: `echo "Hello K8s Storage" > /data/test.txt`.

**Part 3: The Survival Test**
1. Delete the Pod: `kubectl delete pod <pod-name>`.
2. Create a *new* Pod (with a different name) that uses the same `data-pvc`.
3. Exec into the new pod and run `cat /data/test.txt`.
4. Observe that the data survived! You have successfully decoupled the data's lifecycle from the pod's lifecycle.

**Part 4: Clean up & Reclaim**
1. Delete your PVC.
2. Check if the underlying PV still exists (this depends on the `reclaimPolicy` of your storage class).
3. Discuss: If you are running a Production Database, why would you set the reclaim policy to `Retain`?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Multi-Node limitations. `ReadWriteOnce` volumes can usually only be attached to a single Node at a time. If you have two pods on different nodes trying to use the same PVC, one will fail to start.
- **Gotcha 2:** Pending PVCs. If your storage request is larger than what the cluster allows (e.g., requesting 100Ti on a local minikube), the PVC will stay `Pending` forever.

### Reflection Question
Why is Kubernetes considered "Stateless by design," and what operational complexities are introduced when we force it to handle "State" (like a Database)?
