# Exercise 006 - Helm Charts & Package Management

### Objective
Scale your deployments with templates. Master **Helm**, the "Package Manager for Kubernetes." Learn how to use pre-built charts to deploy complex applications (like Redis or ingress-nginx) and build your own reusable templates with variables.

### Core Concepts to Master
- **Helm Chart:** A collection of files that describe a related set of Kubernetes resources.
- **Repository:** A place where charts can be collected and shared (e.g., Artifact Hub).
- **Values.yaml:** The file where you define configuration variables for a chart.
- **Templating:** Using Go template logic (`{{ .Values.name }}`) to dynamically generate YAML manifests.

### Research Topics
- "What is Helm and why do we use it?"
- "Installing apps with Helm: repo add, install, upgrade"
- "Helm template functions (range, if, default)"

---

### The Practical Challenge

**Part 1: Installing a 3rd Party Chart**
1. Install the Helm CLI.
2. Add the Bitnami repository: `helm repo add bitnami https://charts.bitnami.com/bitnami`.
3. Search for a Redis chart: `helm search repo redis`.
4. Install Redis into your cluster: `helm install my-cache bitnami/redis`.
5. Observe the output. Note how a single Helm command created multiple pods, services, secrets, and configurations.

**Part 2: Customizing the Install**
1. Create a `my-values.yaml` file.
2. Override a value (e.g., change the replica count or disable password authentication).
3. Upgrade your existing release: `helm upgrade my-cache bitnami/redis -f my-values.yaml`.

**Part 3: Creating your First Chart**
1. Scaffolding: `helm create my-app`.
2. Explore the directory structure: `Chart.yaml`, `values.yaml`, and the `templates/` folder.
3. Update `templates/deployment.yaml` to include a custom label that pulls from `values.yaml`.
4. Run `helm template .` to see the generated YAML locally without actually deploying it.

**Part 4: Rollbacks**
1. Intentionally introduce a bug in your chart (e.g., an invalid image) and deploy it.
2. Observer the release failure.
3. Use `helm history my-app` to see your version history.
4. Use `helm rollback my-app 1` to return to the previous working state.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Release Names. Every time you run `helm install`, you must provide a unique release name. If you delete a release, its name is freed up, but some persistent resources might stay behind.
- **Gotcha 2:** Whitespace in YAML. YAML is indentation-sensitive. Go templates often introduce extra newlines or spaces. Use `{{-` and `-}}` in your templates to trim whitespace.

### Reflection Question
How does Helm solve the problem of "Configuration Drift" in teams where multiple developers are editing raw YAML files?
