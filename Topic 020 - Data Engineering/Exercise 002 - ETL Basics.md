# Exercise 002 - ETL Basics with Python/SQL

### Objective
Master the "Engine" of data movement. Learn how to Extract, Transform, and Load (ETL) data between different systems (e.g., from CSVs to Postgres) using **Python (Pandas/DuckDB)** and **SQL**, building a reliable pipeline for clean, analysis-ready data.

### Core Concepts to Master
- **The ETL Flow:**
  - **Extract:** Reading data from source systems (APIs, Databases, Logs).
  - **Transform:** Cleaning and formatting data, handling missing values.
  - **Load:** Moving the data into a target system (a Data Warehouse).
- **Pandas:** A powerful Python library for data manipulation and analysis.
- **SQL for Transformation:** Using `JOINs`, `GROUP BY`, and `Window Functions` to calculate metrics inside the database.
- **Data Types:** Ensuring consistency when moving numeric data from strings in a CSV to integers in a database.

### Research Topics
- "Comparing ETL vs ELT (Extract, Load, Transform)"
- "Using Python's Pandas for simple ETL"
- "DuckDB: The in-process analytical database"
- "Handling null values in Python and SQL"

---

### The Practical Challenge

**Part 1: The Extraction Task**
1. Download a raw CSV dataset (e.g., "Daily Sales Data" or "Weather Data").
2. Write a Python script to read the CSV into a **Pandas DataFrame**.
3. Inspect the data: `df.info()` and `df.head(10)`. Identify missing values or incorrect data types.

**Part 2: The Transform Task**
1. Clean the data using Python:
   - Fill in or drop missing values (e.g., `df.fillna(0)`).
   - Convert date strings into a proper `datetime` format.
   - Filter out invalid rows (e.g., negative prices).
2. Calculate a new column (e.g., `TotalProfit = Revenue - Cost`).

**Part 3: The Loading Task**
1. Set up a local Postgres database (or use **SQLite**/ **DuckDB** for simplicity).
2. Write the cleaned DataFrame to a database table.
3. Verify the load: Use SQL to run a simple query: `SELECT count(*) FROM sales_table`.

**Part 4: Scaling to SQL**
1. Instead of doing all cleaning in Python, load the *raw* data into a table.
2. Write a SQL script that performs the same transformations (e.g., `COALESCE(price, 0)`).
3. Discuss: Why is it often faster to load raw data and then transform it using the database's own CPU (ELT)?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Memory Limits. Pandas loads the entire dataset into RAM. If you are processing a 10GB CSV on an 8GB laptop, your script will crash. Use "Chunking" or a tool like **Polars** or **Dask** for large data.
- **Gotcha 2:** Schema Drift. If the source CSV unexpectedly changes a column name (e.g., `Date` to `Sale_Date`), your script will break. Always validate the input schema first.

### Reflection Question
How do the error-handling requirements for Data Pipelines differ from the error-handling requirements of a real-time Web API?
