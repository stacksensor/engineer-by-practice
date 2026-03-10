# Exercise 005 - Identity & OIDC (OpenID Connect)

### Objective
Standardize user and service authentication. Learn how to integrate Kubernetes with an external **Identity Provider (IdP)** like Okta, Google, or GitHub using **OIDC**, and explore how "Workload Identity" allows pods to authenticate with Cloud services (like AWS S3) without using static Access Keys.

### Core Concepts to Master
- **OIDC (OpenID Connect):** An identity layer on top of the OAuth 2.0 protocol that allows you to verify the identity of an end-user based on authentication performed by an Authorization Server.
- **JWT (JSON Web Token):** The standard format used for the ID Token in OIDC.
- **Issuer URL & Client ID:** Configuration parameters needed by K8s to trust an external provider.
- **IRSA / Workload Identity:** A mechanism where a K8s ServiceAccount is linked to a Cloud IAM Role, allowing a Pod to "Assume" that role.

### Research Topics
- "Configuring OIDC for Kubernetes"
- "How do JSON Web Tokens work?"
- "EKS Pod Identity vs IRSA"
- "Dex: A federated OpenID Connect provider"

---

### The Practical Challenge

**Part 1: Deconstructing a JWT**
1. Find a sample JWT (or generate one using a service like `jwt.io`).
2. Identify the three parts: Header, Payload, and Signature.
3. Decode the Payload and find common claims like `sub` (Subject), `iss` (Issuer), and `exp` (Expiration).
4. Discuss: Why can the user see the content of the token but cannot modify their permissions within it?

**Part 2: OIDC Flow (Conceptual)**
1. Trace the flow: 
   - User runs `kubectl login`. 
   - Browser opens to Identity Provider. 
   - User authenticates. 
   - IdP sends a Token back to the local `kubeconfig`.
   - `kubectl` sends the Token to the K8s API Server.
   - API Server verifies the signature against the IdP's public key.

**Part 3: Workload Identity Setup**
1. Research how to link a K8s ServiceAccount to an AWS IAM Role (IRSA) or GCP Service Account.
2. Annotate a ServiceAccount: `eks.amazonaws.com/role-arn: arn:aws:iam::...`.
3. Deploy a pod using that ServiceAccount.
4. Try to access a cloud resource (e.g., list an S3 bucket or a Cloud Storage bucket).
5. Explain how this is more secure than putting `AWS_ACCESS_KEY_ID` into a K8s Secret.

**Part 4: Federated Identity with Dex**
1. Research the **Dex** project. 
2. Explain how Dex acts as a "Connector" that allows you to use your LDAP or GitHub account to log into a cluster that only supports OIDC.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Clock Skew. JWT tokens have an expiration time. If your server's clock is 5 minutes behind the Identity Provider's clock, the token might be rejected as "Not valid yet" or "Already expired."
- **Gotcha 2:** Group Scopes. Sometimes the IdP sends the user's groups in the token, but K8s doesn't recognize the claim name (e.g., looking for `groups` but the IdP sends `cognito:groups`). You must configure the API server's `--oidc-groups-claim` flag.

### Reflection Question
Why is "Short-lived credentials" (tokens) considered significantly more secure than "Static credentials" (passwords/keys) in a modern cloud-native environment?
