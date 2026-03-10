# Exercise 003 - Secret Management with Vault

### Objective
Graduate from simple K8s Secrets to industrial-grade identity and secret management. Learn how to use **HashiCorp Vault** to store, rotate, and audit access to sensitive data, and explore how applications can retrieve secrets dynamically without storing them in YAML files.

### Core Concepts to Master
- **Dynamic Secrets:** Generating short-lived credentials (like a database password) that expire automatically.
- **Leasing & Revocation:** Every secret in Vault has a "lease." If the lease expires, the secret is revoked.
- **Policy Enforcement:** Using HCL (HashiCorp Configuration Language) to define fine-grained access to secret paths (e.g., `secret/data/production/*`).
- **Unsealing:** The security mechanism where multiple "Key Holders" must provide their keys to unlock the Vault after a restart.

### Research Topics
- "What is HashiCorp Vault and how does it work?"
- "Vault vs Kubernetes Secrets"
- "Understanding the Vault sidecar injector for K8s"

---

### The Practical Challenge

**Part 1: Setting up the Vault**
1. Install Vault locally or use a managed instance. (For testing, run it in `-dev` mode: `vault server -dev`).
2. Set your environment: `export VAULT_ADDR='http://127.0.0.1:8200'`.
3. Check the status: `vault status`.

**Part 2: Storing and Reading**
1. Enable the KV (Key-Value) engine version 2: `vault secrets enable -path=secret kv-v2`.
2. Store your first secret: `vault kv put secret/apps/my-app api_key="super-secret-123"`.
3. Retrieve the secret: `vault kv get secret/apps/my-app`.
4. Update the secret and view the version history using the `get -version` flag.

**Part 3: Access Policies**
1. Create a `policy.hcl` file that allows `read` access only to `secret/data/apps/my-app`.
2. Upload the policy: `vault policy write app-readonly policy.hcl`.
3. Create a temporary Token with that policy: `vault token create -policy="app-readonly"`.
4. Try to read a different path using that token and observe the "Permission Denied" error.

**Part 4: K8s Integration (Conceptual)**
1. Research how a "Sidecar Injector" works in Kubernetes.
2. Discuss the flow: The Pod starts -> Vault Injector sees the annotation -> Injector adds a sidecar to the Pod -> Sidecar fetches the secret from Vault and writes it to a local disk path (like `/vault/secrets/config`) for the app to read.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Secret Paths in KV-v2. When using the v2 engine, the API/CLI path often requires a hidden `data/` or `metadata/` prefix (e.g., `secret/data/foo`). Vault handles this automatically in the CLI, but manual API calls will fail without it.
- **Gotcha 2:** The Seal. In production, if your Vault server restarts, it starts in a `Sealed` state. No secrets can be read until the shard holders provide their keys.

### Reflection Question
How does using "Dynamic Secrets" (where every app gets its own unique, short-lived password) prevent a single compromised service from taking down your entire infrastructure?
