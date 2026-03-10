# Exercise 005 - Data Transformation with dbt

### Objective
Apply Software Engineering principles to Data Engineering. Master **dbt (data build tool)** to version control your SQL transformations, run tests on your data quality, and automatically generate documentation for your internal data models.

### Core Concepts to Master
- **The "T" in ELT:** dbt only handles the **Transformation** of data that is already inside your warehouse.
- **Models:** SQL files (`.sql`) that describe how to transform raw tables into "Clean" tables.
- **Macros:** Jinja templates that allow you to reuse SQL logic like variables or loops.
- **Materializations:** Deciding if a model should be a `view`, a `table`, or an `incremental` update.
- **Lineage:** Tracking the "Parent -> Child" relationship between different data models.

### Research Topics
- "What is dbt and how is it different from traditional ETL?"
- "The dbt project structure (models, seed, snapshots)"
- "Using the ref() function in dbt"

---

### The Practical Challenge

**Part 1: Scaffolding a Project**
1. Install dbt-core and a connector (e.g., `dbt-postgres` or `dbt-duckdb`).
2. Run `dbt init my_analytics`. 
3. Configure your `profiles.yml` to connect to your local or cloud database.

**Part 2: The First Model**
1. Create a "Raw" table in your database with some dummy sales data.
2. In your dbt project, create a file `models/stg_sales.sql`.
3. Write a simple SQL query to clean the column names (e.g., `SELECT sale_id as id, ...`).
4. Run `dbt run`. Check your database—dbt has automatically created the table or view for you!

**Part 3: Using the ref() Function**
1. Create a second model `models/daily_revenue.sql`.
2. Use the `{{ ref('stg_sales') }}` macro to build this new model on top of your first one.
3. Run `dbt run` again. Observe that dbt automatically runs the parent model before the child model.

**Part 4: Data Testing**
1. Create a `schema.yml` file.
2. Add a `not_null` and `unique` test for the `id` column.
3. Run `dbt test`. 
4. Intentionally add a duplicate row to your raw data and run the test again. Watch it fail.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Hard-coding table names. Never use `FROM my_database.raw_table`. Always use `{{ source('raw', 'table') }}` or `{{ ref('stg_table') }}` so dbt can manage the dependencies and handle development vs. production environments.
- **Gotcha 2:** View vs Table. By default, dbt creates "Views." If your data is huge, querying these views repeatedly will be slow and expensive. Switch to `table` or `incremental` materializations for better performance.

### Reflection Question
How does dbt help "Data Analysts" and "Software Engineers" work together on the same codebase using Git?
