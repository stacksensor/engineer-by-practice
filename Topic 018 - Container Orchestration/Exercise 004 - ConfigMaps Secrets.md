# Exercise 004 - ConfigMaps & Secrets

### Objective
Decouple configuration from code. Use **ConfigMaps** to store non-sensitive configuration data (like environment names) and **Secrets** to store sensitive data (like API keys or passwords), injecting them into your containers at runtime.

### Core Concepts to Master
- **ConfigMap:** An API object used to store non-confidential data in key-value pairs.
- **Secret:** Similar to a ConfigMap but used to store sensitive information, encoded in Base64 (though not encrypted by default at rest).
- **Environment Injection:** Mapping keys from a ConfigMap/Secret directly to environment variables in a container.
- **Volume Injection:** Mounting ConfigMap/Secret data as files within a directory in the container.

### Research Topics
- "Injecting ConfigMaps into Pods"
- "Are Kubernetes Secrets secure?"
- "Scaling configuration with Helm"

---

### The Practical Challenge

**Part 1: Creating the Config**
1. Create a ConfigMap from the command line: `kubectl create configmap app-config --from-literal=DB_HOST=localhost --from-literal=LOG_LEVEL=info`.
2. Create a Secret: `kubectl create secret generic app-secrets --from-literal=API_KEY=123456`.
3. Verify them: `kubectl get configmap app-config -o yaml` and `kubectl get secret app-secrets -o yaml`.
4. Note that the Secret values are shown in Base64. (Try decoding it: `echo <base64-string> | base64 --decode`).

**Part 2: Environment Injection**
1. Create a Pod manifest where the container uses `envFrom` to load all keys from the `app-config` ConfigMap.
2. Manually add one environment variable named `SECRET_KEY` pulled from the `app-secrets` Secret using `secretKeyRef`.
3. Apply the pod and run `kubectl exec <pod-name> -- env`. Verify all variables are present.

**Part 3: The Volume Mount**
1. Update your Pod to mount the `app-config` ConfigMap as a volume at `/etc/config`.
2. Apply the change.
3. Run `ls /etc/config` inside the container. Notice there is a file for every key in the ConfigMap.
4. Read a file: `cat /etc/config/DB_HOST`.

**Part 4: Real-time Updates**
1. Update the value of `DB_HOST` in your ConfigMap using `kubectl edit cm app-config`.
2. Wait 60 seconds.
3. Check the file `/etc/config/DB_HOST` inside the container again. Notice that K8s automatically updated the file! (Note: Environment variables DO NOT update automatically without a pod restart).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Base64 is NOT Encryption. K8s secrets are just encoded. Anyone with `kubectl` access to the namespace or access to ETCD can read them. Use external tools like HashiCorp Vault for real security.
- **Gotcha 2:** Mount Paths. If you mount a ConfigMap to `/etc`, it will overwrite the entire `/etc` directory in the container, potentially breaking the OS. Always mount to a specific, unique subdirectory.

### Reflection Question
Why is it risky to keep a Secret mounted as a Volume if your application is vulnerable to an "arbitrary file read" exploit?
