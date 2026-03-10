# Exercise 006 - Image Scanning & Supply Chain

### Objective
Secure the code before it ever reaches the cluster. Master **Container Image Scanning** using tools like **Trivy**, and explore the "Supply Chain Security" concepts like **Software Bill of Materials (SBOM)** and **Cosign** (image signing).

### Core Concepts to Master
- **CVE (Common Vulnerabilities and Exposures):** A standardized list of publicly disclosed cybersecurity vulnerabilities.
- **Image Scanners:** Automated tools that scan a container's OS packages and application dependencies for known CVEs.
- **SBOM (Software Bill of Materials):** A complete inventory of every library, package, and component inside your image.
- **Image Signing (Cosign):** Using a private key to "Sign" an image at the end of a CI build, ensuring that only "Verified" images are ever allowed to run in production.

### Research Topics
- "What is Trivy and how to use it?"
- "The importance of SBOM in Log4j style exploits"
- "Cosign vs Docker Content Trust"

---

### The Practical Challenge

**Part 1: Scanning for Vulnerabilities**
1. Install **Trivy**.
2. Scan a notoriously vulnerable image: `trivy image node:14`. Note the number of "Critical" and "High" vulnerabilities.
3. Now, scan a minimal image: `trivy image node:alpine`. Compare the results.
4. Scan a "Distroless" image: `trivy image gcr.io/distroless/nodejs:latest`. Note the incredibly small number of vulnerabilities.

**Part 2: Integrating with CI**
1. Research how to add a `trivy` step to a GitHub Actions or GitLab pipeline.
2. Discuss the policy: "Fail the build if any Critical or High vulnerabilities are found."
3. Think about "Vulnerability Fatigue." How would you handle a vulnerability that has no available fix yet?

**Part 3: Generating an SBOM**
1. Use `trivy image --format cyclonedx --output sbom.json <image-name>` to generate your first SBOM.
2. Open the JSON file. Notice how it lists every single library (including transitive dependencies) and their versions.
3. Explain why this is essential for "Emergency Audits" when a new vulnerability (like a zero-day) is discovered.

**Part 4: Digital Signatures**
1. Research the **Cosign** tool from the Sigstore project.
2. Generate a key pair: `cosign generate-key-pair`.
3. (Optional/Conceptual): Sign a local image: `cosign sign --key cosign.key <registry/my-image>`.
4. Discuss how an "Admission Controller" in Kubernetes (like Kyverno) can be configured to block any image that isn't signed by your company's private key.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Scanning Layers vs. Binaries. Some scanners only check the OS packages (`apk`, `apt`). They might miss a vulnerable Node.js library (`package.json`) or a Go binary inside. Always use a tool that supports language-specific scanning.
- **Gotcha 2:** Scanner Staleness. A scanner is only as good as its CVE database. Always ensure your scanning tool is updated before running a scan.

### Reflection Question
Why is "Scanning on build" (CI) not enough, and why must you also perform "Periodic scanning" of images that are *already* running in production?
