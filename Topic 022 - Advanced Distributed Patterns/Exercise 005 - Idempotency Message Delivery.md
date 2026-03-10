# Exercise 005 - Idempotency & Message Delivery

### Objective
Ensure "Exactly Once" behavior in a "Maybe Serviceable" world. Master **Idempotency**—the property where an operation can be performed multiple times without changing the result beyond the initial application—and learn how to handle duplicate messages in distributed queues.

### Core Concepts to Master
- **At-Most-Once:** The message is sent but might be lost. Never duplicated.
- **At-Least-Once:** The message is guaranteed to arrive, but might arrive multiple times. (The industry default).
- **Exactly-Once:** The holy grail where a message arrives exactly once. (Usually achieved via At-Least-Once + Idempotency).
- **Idempotency Key:** A unique identifier provided by the client (e.g., `request_id: 123`) that the server uses to check if it has already processed that specific request.
- **Side Effects:** Why read operations (`GET`) should always be naturally idempotent, while write operations (`POST`) require explicit keys.

### Research Topics
- "What is idempotency in REST APIs?"
- "Implementing idempotency keys with Redis"
- "Stripe's guide to Idempotency"

---

### The Practical Challenge

**Part 1: The Double-Charge Disaster**
1. Imagine an API call: `POST /payments {amount: 100}`.
2. The user clicks "Submit." The server processes the payment but the user's internet drops before they get the "Success" response.
3. The user clicks "Submit" again.
4. Without idempotency, they are charged twice ($200). Discuss: How do you solve this?

**Part 2: The Idempotency Key (Code)**
1. Create a server-side logic:
   - When a request arrives, check if `Header: X-Idempotency-Key` exists.
   - Look up the key in a database (like Redis).
   - If it exists, return the *stored* response from the previous success.
   - If not, process the request, store the result in Redis, and return it.
2. Set a TTL (Time To Live) on the key (e.g., 24 hours).

**Part 3: Distributed Queue Duplicates**
1. Research how RabbitMQ or Kafka handles "Retries."
2. Imagine a worker processes an order but crashes *just before* acknowledging the message. The queue will re-send the message to another worker.
3. Explain how the worker can use the `order_id` in the database to ensure it doesn't process the same order twice.

**Part 4: Natural Idempotency**
1. Discuss why `SET temperature = 25` is idempotent, but `INCREMENT temperature BY 1` is not.
2. How can you redesign non-idempotent operations to be idempotent? (e.g., passing the "expected current version" or "previous state" in the request).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Race Conditions. If two identical requests arrive at the *exact same millisecond*, your check might fail and both might process. You must use a "Distributed Lock" or a `SELECT FOR UPDATE` on the idempotency key.
- **Gotcha 2:** Changing the Body. If a user sends a request with `Key: 123` and `Amount: 100`, then later sends `Key: 123` but `Amount: 500`, the server might return the old "Success (100)" message. This is a payload mismatch. Your server should validate that the body hasn't changed for the same key.

### Reflection Question
How does idempotency act as a "Safety Net" for distributed systems that rely on automatic retries?
