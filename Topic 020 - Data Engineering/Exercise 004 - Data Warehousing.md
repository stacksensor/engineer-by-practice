# Exercise 004 - Data Warehousing (BigQuery / Snowflake)

### Objective
Scale to Petabytes. Explore the modern Cloud Data Warehouse (CDW) architecture. Learn how to manage storage and compute separately using tools like **Google BigQuery** or **Snowflake**, and master the "Billing" mindset where every SQL query costs money.

### Core Concepts to Master
- **Serverless Analytics:** Querrying massive amounts of data without managing any actual servers.
- **Partitioning & Clustering:** Grouping data together on disk to ensure your query only reads the specific "Slices" it needs, drastically reducing costs.
- **Federated Queries:** Querying data directly from an S3 bucket or Google Cloud Storage without "Importing" it into the database first.
- **UDFs (User Defined Functions):** Writing your own functions in JavaScript or SQL to perform complex logic inside the warehouse.

### Research Topics
- "BigQuery vs Snowflake architectural differences"
- "How Does BigQuery storage billing work?"
- "What is a Partitioned Table in Snowflake?"

---

### The Practical Challenge

**Part 1: The First Query**
1. Access a public dataset in BigQuery (e.g., `github_repos` or `chicago_taxi_trips`).
2. Run a simple `SELECT * FROM ... LIMIT 10`. 
3. Note how the UI tells you "This query will process 2.4 GB."
4. Discuss: Why is `SELECT *` considered "Dangerous" in a cloud data warehouse?

**Part 2: Optimizing for Cost**
1. Refine your query to only select specific columns (e.g., `repo_name`, `language`).
2. Note the new "Data processed" estimate. It should be drastically lower. 
3. Run a query that uses a `WHERE` clause on a date column. If the table is **Partitioned**, this query will be significantly cheaper.

**Part 3: Loading and External Tables**
1. Create a CSV file and upload it to a Cloud Bucket (S3/GCS).
2. Create an "External Table" in your warehouse that points to that bucket.
3. Query the external table. Explain how this allows you to build a "Data Lake" where the data lives in cheap storage but is still queryable via SQL.

**Part 4: Managing Roles**
1. In the Cloud Console, look at the IAM roles for your warehouse (e.g., `BigQuery Data Viewer` vs `BigQuery Admin`).
2. Create a "Restricted Service Account" that can only read one specific dataset but cannot delete anything.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Flattening Arrays. Modern warehouses often store complex JSON objects or Arrays. To query these, you must use special commands like `UNNEST` in BigQuery or `FLATTEN` in Snowflake.
- **Gotcha 2:** Query Slots. If 100 people try to run heavy analytical queries at the same time, your performance will drop. Most warehouses have "Concurrency limits" that you need to monitor.

### Reflection Question
If your company has 100 Terabytes of data, why might it be cheaper to store it in a Cloud Warehouse (like Snowflake) than to buy and maintain your own physical servers and hard drives?
