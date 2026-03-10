# Exercise 001 - Data Modeling & Storage Types

### Objective
Learn the foundation of data architecture. Explore the fundamental differences between **Relational (OLTP)**, **Document**, **Columnar (OLAP)**, and **Key-Value** storage models, and learn how to choose the right data model based on the "Read vs Write" patterns of your application.

### Core Concepts to Master
- **OLTP (Online Transactional Processing):** Optimized for high-frequency, low-latency small writes (e.g., Postgres, MySQL).
- **OLAP (Online Analytical Processing):** Optimized for complex queries across large datasets (e.g., BigQuery, ClickHouse).
- **Normalization vs. Denormalization:** Reducing redundancy through relations vs improving performance by duplicating data.
- **Star Schema:** A specific data modeling technique for analytics involving "Facts" (measurable events) and "Dimensions" (descriptive context).

### Research Topics
- "OLTP vs OLAP differences for data engineers"
- "Introduction to Dimensional Modeling"
- "When to use a Columnar database?"
- "The CAP Theorem: Consistency, Availability, Partition Tolerance"

---

### The Practical Challenge

**Part 1: The Normalized Store (OLTP)**
1. Design a simple schema for an E-commerce store with `Users`, `Orders`, and `Products`.
2. Ensure it is in **3rd Normal Form (3NF)** (no duplicated data, everything linked by foreign keys).
3. Discuss: Why is this perfect for a web app handling millions of user logins and purchases?

**Part 2: The Analytical Challenge (OLAP)**
1. Imagine you need to run a report: "Total revenue per city per month for the last 5 years."
2. Analyze how many "Joins" a relational database would need to do to answer this.
3. Research **Columnar Storage**. Explain why reading only the "Price" and "City" columns is faster than reading the entire row in a traditional database.

**Part 3: Designing a Star Schema**
1. Take your E-commerce schema and transform it into a **Star Schema** for an Analytics dashboard.
2. Define a **Fact Table**: `Fact_Sales` (containing keys and metrics like `price`, `quantity`).
3. Define **Dimension Tables**: `Dim_Date`, `Dim_Product`, `Dim_Location`.
4. Discuss the concept of "Slowing Changing Dimensions" (SCD).

**Part 4: Real-world Mapping**
1. Search for a public dataset (e.g., from Kaggle or AWS Public Datasets).
2. Identify which columns are "Dimensions" and which are "Facts."
3. Sketch a diagram of how you would model this data in a Big Data warehouse.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-normalization. If you have to join 15 tables to display a simple user profile, your app will be slow. Don't be afraid of "Controlled Redundancy."
- **Gotcha 2:** Premature Scaling. Don't build a complex Data Lake for 10,000 rows. A simple Postgres database can handle millions of analytical rows before you need "Big Data" tools.

### Reflection Question
Why is a database that is incredibly fast at "Updating a single user's password" (OLTP) usually very slow at "Averaging the age of 50 million users" (OLAP)?
