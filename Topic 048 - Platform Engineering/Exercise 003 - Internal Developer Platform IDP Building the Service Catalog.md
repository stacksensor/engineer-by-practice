# Exercise 003 - Internal Developer Platform (IDP): Building the "Service Catalog"

### Objective
Map the kingdom. Learn to build a **Service Catalog**—the "Yellow Pages" of your company—where every Microservice, its Owner, its API, and its "Health" can be found in one single UI.

### Core Concepts to Master
- **Service Catalog:** The single source of truth for "What runs in production?"
- **Ownership:** Linking every microservice to its **Team (E.g., "Team Phoenix")**.
- **The "Service" Lifecycle:** 
   - 1. **Propose** (RFC).
   - 2. **Create** (Scaffolder).
   - 3. **Run** (K8s).
   - 4. **Observe** (Grafana).
   - 5. **Deprecate** (Deletion).
- **Extending Backstage:** Using **Backstage Search** to find the "API Documentation" for a service you didn't build.

### Research Topics
- "Backstage Plugins: How to add your own into the portal"
- "Service Catalog with a YAML file: `catalog-info.yaml`"
- "Software Templates: Generating an App with 1 Click"
- "Metrics in Backstage: Showing Grafana in your developer portal"

---

### The Practical Challenge

**Part 1: The "Search" Disaster (Scenario)**
1. You need to call the "Payment API."
2. **Without a Portal:** You ask in Slack. 10 people answer. You find 5 different links. 3 are dead.
3. **With a Portal:** You search "Payment."
4. Result: 1 Service. **Owner:** Sarah. **Link:** `/payment-api`. **Docs:** Swagger.
5. Discuss: Does Sarah spend her whole day answering "Where is the API?" 
6. Answer: She spends 0 time. The portal answers for her. **Sarah is now a more productive engineer.**

**Part 2: The "YAML" Truth**
1. You create a file: **`catalog-info.yaml`**. 
2. In it, you name your service "Order-Service" and link it to "Team-Alpha."
3. Discuss: Why should the "Code" (YAML) be in the same repo as the service?
4. Answer: Because if the Team name changes, the YAML changes in the PR, and the Portal updates automatically.

**Part 3: The "Scaffolder" Builder**
1. Research **Backstage Software Templates**. 
2. Discuss: If you build a "Go API" template, can you make it create a **GitHub Repo**, a **CI pipeline**, and a **K8s Deployment**?
3. Answer: Absolutely. That is the definition of **"Self-Service Infrastructure."**

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Stale" Portal. If developers don't update their YAML files, the portal is worthless. (Solution: Use **Automated Scanners** to detect old services).
- **Gotcha 2:** Information Overload. If 500 services are in the catalog, how do you find the "Important" ones? (Solution: Use **Custom Filters** and **Favorites**).

### Reflection Question
Why is a "Service Catalog" the antidote to the 'Microservices Mess'? (Answer: Because it adds a Layer of Governance and Visibility to 100 separate folders that would otherwise be chaos).
