# Exercise 006 - Network Security & TLS Deep Dive

### Objective
Secure the wire. Master **TLS (Transport Layer Security)**. Understand how Public/Private keys, Certificates, and Handshakes work to provide Confidentiality, Integrity, and Authenticity. Learn how to manage certificates with **Let's Encrypt** and how to debug TLS handshake failures.

### Core Concepts to Master
- **Symmetric vs Asymmetric Encryption:** 
  - Asymmetric (RSA/ECC) for exchanging keys.
  - Symmetric (AES) for the actual high-speed data transfer.
- **The TLS Handshake:** Client Hello -> Server Hello -> Key Exchange -> Change Cipher Spec.
- **Certificate Authorities (CA):** Why we "Trust" a certificate because it was signed by a trusted 3rd party.
- **Perfect Forward Secrecy (PFS):** Ensuring that if a server's private key is stolen *today*, it cannot be used to decrypt traffic recorded *yesterday*.

### Research Topics
- "How does the TLS handshake work? (Simplified)"
- "What is a Certificate Chain of Trust?"
- "Using OpenSSL to inspect certificates"
- "Cert-manager for Kubernetes"

---

### The Practical Challenge

**Part 1: Inspecting the Certificate**
1. Use the `openssl` command to view the certificate for a site like google.com:
   `openssl s_client -connect google.com:443 -showcerts`
2. Identify the "Subject," the "Issuer" (CA), and the "Expiration Date."

**Part 2: The "Self-Signed" Warning**
1. Generate your own private key and self-signed certificate using OpenSSL.
2. Configure a local web server (like NGINX or a Node.js app) to use this certificate.
3. Access the site in your browser. Observe the "Your connection is not private" warning.
4. Explain why the browser trusts `google.com` but not your local certificate.

**Part 3: Automating with Let's Encrypt**
1. Research how **Certbot** and the **ACME protocol** work.
2. Explain the "Challenge" process (HTTP vs DNS) that proves you own a domain before a certificate is issued.

**Part 4: Debugging Handshakes**
1. Research "Cipher Mismatch" errors. 
2. Discuss: If an old browser (IE6) tries to connect to a modern server that only supports TLS 1.3, what happens?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Expired Certificates. This is the #1 cause of major production outages (including in big companies like Spotify and Microsoft). Always automate your renewals!
- **Gotcha 2:** The "Chain" problem. If you only provide your certificate but not the "Intermediate" certificates from the CA, some devices will reject the connection because they cannot trace the trust back to the Root.

### Reflection Question
Why is "Terminating SSL" at the Load Balancer (instead of the app server) considered a standard performance optimization?
