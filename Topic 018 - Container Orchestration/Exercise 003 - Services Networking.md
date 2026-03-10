# Exercise 003 - Services & Networking

### Objective
Enable communication. Learn how to use Kubernetes **Services** to provide a stable IP address and DNS name for a group of ephemeral Pods, and explore the internal cluster network that allows services to talk to each other.

### Core Concepts to Master
- **Service (Svc):** An abstraction that defines a logical set of Pods and a policy by which to access them.
- **ClusterIP:** The default service type, providing an internal IP accessible only within the cluster.
- **NodePort:** Exposing a service on a static port on each Node’s IP, making it accessible from outside the cluster.
- **Service Discovery:** Using the built-in CoreDNS to find services by name (e.g., `http://my-service`) instead of IP.

### Research Topics
- "Kubernetes Service types explained"
- "How does Kube-proxy manage networking?"
- "The difference between TargetPort and Port in a Service"

---

### The Practical Challenge

**Part 1: The Internal Load Balancer**
1. Create a Deployment (or ReplicaSet) with 3 replicas of an app that returns its own hostname (e.g., `k8s.gcr.io/echoserver:1.4`).
2. Create a Service of type `ClusterIP` named `echo-service` that targets these pods.
3. Verify the service exists: `kubectl get svc`. Note the `CLUSTER-IP`.

**Part 2: Testing Connectivity**
1. Create a "Temporary" pod to act as a client: `kubectl run curl-client --image=curlimages/curl -it --rm -- sh`.
2. From inside the client pod, try to curl the service's ClusterIP: `curl <CLUSTER-IP>:8080`.
3. Now, try to curl by name: `curl echo-service:8080`. 
4. Repeat the curl multiple times. Notice that the response changes to show different hostnames. The Service is performing internal Load Balancing!

**Part 3: External Access (NodePort)**
1. Change your service type to `NodePort`. 
2. Get the assigned NodePort: `kubectl get svc echo-service`. It will be a number between 30000-32767.
3. Access the service from your host machine (outside the cluster) using the Node's IP and the NodePort.

**Part 4: Headless Services**
1. Research "Headless Services" (setting `clusterIP: None`).
2. Update your service to be headless.
3. Use the `nslookup echo-service` command from your client pod. Observe that it returns the IPs of all 3 individual pods instead of a single service IP. This is useful for StatefullSets and Databases.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** TargetPort Mismatch. If your service is listening on port 80 but your application inside the container is listening on port 3000, you must set `targetPort: 3000` in the Service manifest.
- **Gotcha 2:** Selector Miss. If your Service selector doesn't perfectly match the Pod labels, the Service will have 0 "Endpoints." Check with `kubectl get endpoints`.

### Reflection Question
Why are Services necessary in Kubernetes if every Pod already has its own unique IP address?
