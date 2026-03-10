# Exercise 007 - Monitoring & Auto-scaling (HPA)

### Objective
Build a self-scaling cluster. Learn how to use the **Horizontal Pod Autoscaler (HPA)** to automatically increase or decrease the number of pods in a deployment based on CPU or memory usage, ensuring your app stays responsive during traffic spikes.

### Core Concepts to Master
- **Metrics Server:** A cluster-wide aggregator of resource usage data. Without this, the HPA cannot function.
- **Resource Requests & Limits:** Explicitly defining how much CPU/RAM a pod *needs* vs the maximum it is *allowed* to use.
- **Horizontal Pod Autoscaler (HPA):** A controller that adjusts the number of replicas in a deployment based on observed resource utilization.
- **Cluster Autoscaler:** (Conceptual) Expanding the actual Cloud Nodes (VMs) when the cluster runs out of capacity.

### Research Topics
- "How to install metrics-server on minikube"
- "Difference between Requests and Limits in K8s"
- "Scaling pods based on custom metrics"

---

### The Practical Challenge

**Part 1: Defining Limits**
1. Create a Deployment for a heavy app.
2. In the Pod manifest, set `requests` to `100m` CPU and `limits` to `200m` CPU.
3. Apply the deployment.
4. Verify resource usage: `kubectl top pods`. (If this fails, your Metrics Server is not installed).

**Part 2: The HPA Configuration**
1. Create an HPA for your deployment:
   `kubectl autoscale deployment <name> --cpu-percent=50 --min=1 --max=10`.
2. This tells K8s: "If average CPU usage across pods goes over 50% of the *request*, add more pods (up to 10)."
3. Verify: `kubectl get hpa`.

**Part 3: The Load Test**
1. Start a "Load Generator" pod that runs an infinite loop of heavy calculations.
2. Watch your HPA status: `kubectl get hpa -w`.
3. Notice the `TARGETS` percentage rising. 
4. Observe your deployment: `kubectl get deployment -w`. You should see the `REPLICAS` count increasing automatically.

**Part 4: Scaling Down**
1. Stop the Load Generator.
2. Observe how K8s waits for a "Cool down" period (usually 5 minutes) before deleting the extra pods. 
3. Discuss: Why does K8s wait to scale down instead of doing it immediately?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** No Requests = No HPA. If you don't define `resources.requests` in your pod manifest, the HPA has no baseline and will show `<unknown>` usage, failing to scale.
- **Gotcha 2:** Throttling. If a pod hits its `limit`, K8s will "throttle" its CPU (slow it down) but won't necessarily kill it. If it hits its RAM limit, it will be OOMKilled (Out of Memory Killed).

### Reflection Question
How do the "Requests" and "Limits" you set in Kubernetes directly impact the monthly bill of a company running on a cloud provider like AWS or Google Cloud?
