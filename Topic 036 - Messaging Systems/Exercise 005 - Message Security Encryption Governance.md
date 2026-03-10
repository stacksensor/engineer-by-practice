# Exercise 005 - Message Security & Governance

### Objective
Secure the pipe. Master the security concepts for messaging systems. Learn how to protect sensitive data (like PII) as it travels through a broker. Understand **Encryption in Transit (TLS)**, **Encryption at Rest**, and the concept of **End-to-End Encryption** where the broker itself cannot see the data.

### Core Concepts to Master
- **TLS/SSL:** Protecting messages from being "Sniffed" on the network.
- **SASL/Scram:** Authenticating users to the broker (Name/Password).
- **ACLs (Access Control Lists):** Restricting who can Write to or Read from specific topics (e.g., "Team A can only read from `user_data`").
- **Envelope Encryption:** Encrypting the "Data" field of a message with a custom key BEFORE sending it to the broker.
- **PII Scrubbing:** Automatically removing things like "Social Security Numbers" from events before they hit the log.

### Research Topics
- "Configuring SSL in Apache Kafka"
- "End-to-End Encryption in Messaging Systems"
- "RBAC (Role Based Access Control) in RabbitMQ"
- "The risk of sensitive data in message logs"

---

### The Practical Challenge

**Part 1: The "Logged PII" Disaster**
1. You send an event: `UserUpdated { ssn: "123-456-789" }` to a Kafka topic.
2. Even if the producer and consumer are "Secure," the Kafka broker stores this message on its disk for 7 days.
3. Discuss: If an attacker steals the backup of the Kafka disk, is the data safe? (Answer: No, unless you used **Encryption at Rest**).

**Part 2: Designing an ACL Policy**
1. System: 3 Services (`Order`, `Payment`, `Analytics`).
2. Design a set of rules:
   - `Order Service`: CAN Write to `orders`, CANNOT read from anything.
   - `Payment Service`: CAN Read from `orders`, CAN Write to `payments`.
   - `Analytics Service`: CAN Read from ALL, CANNOT write to anything.
3. Discuss: How does this "Least Privilege" model prevent a bug in the Analytics service from accidentally deleting orders?

**Part 3: End-to-End Encryption (Concept)**
1. The producer encrypts the body using a key from a **KMS** (Key Management Service).
2. The producer sends the encrypted Blob to the broker.
3. The broker cannot read it.
4. The consumer gets the key from KMS and decrypts it.
5. Discuss: Why is this the only way to be 100% compliant in highly regulated industries?

**Part 4: Identifying the security risk**
1. Research **Message Headers**. 
2. Discuss why putting sensitive info (like a Credit Card number) in a "Header" is even more dangerous than putting it in the "Body." (Answer: Headers are often logged in plain text by intermediate routing filters).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Certificate Expiration. If your TLS certificates expire, your entire messaging cluster will stop talking to itself, bringing down your whole system. Use automation (like Let's Encrypt or Vault) to rotate certificates!
- **Gotcha 2:** Performance Hit. Encryption isn't free. Enabling TLS can reduce your message throughput by 10-20% depending on the hardware.

### Reflection Question
Why is the "Audit Log" of WHO sent WHAT message just as important for security as the "Encryption" of the message itself? (Answer: To detect an internal "Bad Actor" or a compromised service).
