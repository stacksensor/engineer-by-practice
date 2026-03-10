# Exercise 003 - CQRS (Command Query Responsibility Segregation)

### Objective
Partition your complexity. Master the **CQRS** pattern, which splits your application into two distinct paths: a **Write Side (Command)** optimized for validation and business logic, and a **Read Side (Query)** optimized for high-speed, aggregated, and denormalized data retrieval.

### Core Concepts to Master
- **Command:** An intention to change system state (e.g., `PlaceOrder`). Commands have side effects and return no data (other than success/failure).
- **Query:** A request for current information (e.g., `GetOrderHistory`). Queries have no side effects and return data.
- **The Segregation:** Using different data models (and potentially different databases) for writes and reads.
- **Eventual Consistency in CQRS:** The "Read" database might be a few milliseconds behind the "Write" database while the data is being synchronized.

### Research Topics
- "What is CQRS and when should you use it?"
- "Synchronizing read and write models in CQRS"
- "Benefits of CQRS for high-traffic applications"

---

### The Practical Challenge

**Part 1: Identifying the Conflict**
1. Imagine an E-commerce product page.
2. The **Write** path requires strict validation: Check stock, check user balance, check shipping rules.
3. The **Read** path requires fast filtering: Sort by price, filter by rating, show related products.
4. Discuss: Why is it difficult to optimize a single SQL table for both of these patterns at the same time?

**Part 2: Designing the Split**
1. Define a Write Model (e.g., a normalized SQL database) that focuses on the individual product details.
2. Define a Read Model (e.g., an Elasticsearch index) that stores a pre-calculated "Product Card" containing the average rating and discounted price.

**Part 3: The Synchronization Logic**
1. Sketch a diagram showing the "Update" flow: 
   - User sends `UpdateProductPrice` command to the API. 
   - API updates the SQL Database.
   - API publishes a `PriceUpdated` event to a Message Queue (like Kafka).
   - A "Projector" microservice reads the event and updates the Elasticsearch index.

**Part 4: Handling the "Lag"**
1. A user updates their product price and hits "Refresh" on the public page. 
2. Because the sync is asynchronous, they still see the old price for a split second.
3. Discuss strategies to hide this from the user (e.g., Optimistic UI updates on the frontend or a "Wait for Sync" header in the API).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-Engineering. CQRS is expensive to build and maintain. Only use it if you have a massive difference in your Read vs. Write patterns or huge scaling requirements. For a simple CRUD app, CQRS is overkill.
- **Gotcha 2:** Lost Events. If the Message Queue fails, your Read model and Write model will get out of sync. You need a way to "Rebuild" the read model from scratch periodically.

### Reflection Question
How does CQRS allow a team to use a SQL database for accounting (where consistency matters) while using a Search Index for product discovery (where speed matters) in the same application?
