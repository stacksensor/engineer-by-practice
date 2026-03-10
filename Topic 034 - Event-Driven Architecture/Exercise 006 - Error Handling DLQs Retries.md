# Exercise 006 - Error Handling: DLQs & Retries

### Objective
Recover gracefully. Master error handling in an asynchronous world. Learn how to deal with consumers that crash or external APIs that are down. Understand the **Retry Pattern**, **Exponential Backoff**, and the **Dead Letter Queue (DLQ)**—the place where "Unprocessable" messages go to die (so you can fix them later).

### Core Concepts to Master
- **The Poison Pill:** A message that is so broken (e.g., malformed JSON) that it crashes the consumer every time it tries to read it.
- **Retry Policy:** Automatically trying again 3 times if an error occurs.
- **Exponential Backoff:** Waiting 1s, then 2s, then 4s, then 8s before retrying, to avoid "hammering" a struggling database.
- **Dead Letter Queue (DLQ):** A separate queue where the broker moves a message after it has failed the maximum number of retries.
- **Compensating Transactions:** Actions taken to "Undo" a partial failure in a multi-step event flow.

### Research Topics
- "RabbitMQ Dead Letter Exchanges (DLX)"
- "Kafka Error Handling Patterns"
- "The risk of infinite retry loops"
- "Monitoring your DLQ: Alerting and Remediation"

---

### The Practical Challenge

**Part 1: The "Poison Pill" Disaster**
1. You have a queue of 1,000 messages.
2. Message #1 is corrupted and crashes your code.
3. Your broker is set to "Auto-retry instantly."
4. Discuss: Why does this one message stop ALL 1,000 messages from being processed? (Answer: The "Head-of-Line" blocking).

**Part 2: Implementing a DLQ Strategy**
1. Design a pseudocode logic:
   - Try processing.
   - If Fail: Increment `retry_count` in the header.
   - If `retry_count` < 5: Wait 10s and put back in queue.
   - If `retry_count` >= 5: Move to `orders_dead_letters`.

**Part 3: The DLQ Triage**
1. You have 50 messages in your DLQ.
2. Discuss: Is a DLQ a "Trash can" or a "Waiting room"? 
3. (Answer: Waiting room. A developer should inspect the DLQ, fix the bug in the code, and then "Replay" the DLQ messages into the main queue).

**Part 4: Identifying "Retry-able" vs "Fatal" errors**
1. Which should you retry?
   - `HTTP 503 (Service Unavailable)` (Answer: Yes, likely temporary).
   - `HTTP 401 (Unauthorized - Bad API Key)` (Answer: No, retrying won't fix your key).
   - `JSON Parse Error` (Answer: No, it's a poison pill).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Duplicate Processing. If your code succeeds in sending an email but crashes *before* it can tell the broker "Done," the broker will send the message again. You will send the email twice. This is why **Idempotency** is required.
- **Gotcha 2:** DLQ Neglect. Many teams set up a DLQ but never look at it. If your DLQ has 1,000,000 messages, your system is effectively "Losing" 1,000,000 user actions.

### Reflection Question
Why is a DLQ more important in an Event-Driven system than in a standard REST API system? (Answer: Because in REST, the user gets an error immediately; in EDA, the error happens in the background where no one is watching).
