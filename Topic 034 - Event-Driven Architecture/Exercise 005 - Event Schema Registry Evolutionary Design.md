# Exercise 005 - Event Schema Registry & Evolutionary Design

### Objective
Don't break the world. Master **Event Schema Management**. Learn how to handle changes to your events (e.g., adding or removing fields) without crashing the services that rely on them. Understand the role of a **Schema Registry** (like Confluent) and how it ensures **Forward** and **Backward Compatibility**.

### Core Concepts to Master
- **The Event Contract:** The agreement between the Producer and Consumer about what fields exist in an event.
- **Serialization Formats:** JSON (Flexible but slow) vs Avro/Protobuf (Strict, fast, and schema-aware).
- **Backward Compatibility:** New code can read old events.
- **Forward Compatibility:** Old code can read new events (usually by ignoring new fields).
- **The Schema Registry:** A centralized tool that stores every version of every event schema and rejects "Breaking Changes."

### Research Topics
- "Confluent Schema Registry overview"
- "Avro vs Protobuf for event streaming"
- "Semantic Versioning (SemVer) for Events"
- "Handling breaking changes in an event-driven system"

---

### The Practical Challenge

**Part 1: The Breaking Change**
1. You have an event `UserSignedUp { id: 1, name: "Alex" }`.
2. You decide to split `name` into `first_name` and `last_name`.
3. Discuss: What happens to the "Email Service" that was looking for the field `name`? (Answer: It crashes or fails to send emails).

**Part 2: The Evolutionary Fix**
1. Research how to make this change safely in 3 steps:
   - Step 1: Add `first_name` and `last_name` but KEEP `name`.
   - Step 2: Update all consumers to use the new fields.
   - Step 3: Once all consumers are safe, remove the old `name` field.

**Part 3: Protobuf/Avro advantages**
1. Research why **Avro** is better than **JSON** for event versioning. 
2. (Answer: Avro requires a schema, and it can detect if a change is "Breaking" before the event is even sent).

**Part 4: Registry Policy**
1. Research the "Backwards" compatibility mode in Confluent Registry. 
2. What happens if you try to delete a "Required" field in this mode? (Answer: The Registry will block the upload with an error).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "God Event." Don't create one giant event `SystemUpdate` that contains every possible field. This makes versioning impossible. Create small, specific events like `UserEmailChanged`.
- **Gotcha 2:** Metadata duplication. Every event should contain standard metadata (e.g., `event_id`, `timestamp`, `correlation_id`, `schema_version`) so consumers know how to handle it.

### Reflection Question
Why is an "Implicit Schema" (just sending JSON) manageable for 2 services but a "Disaster" for 200 services? (Answer: Because you can't coordinate a breaking change across 200 teams simultaneously).
