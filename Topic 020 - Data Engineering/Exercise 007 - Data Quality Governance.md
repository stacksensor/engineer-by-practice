# Exercise 007 - Data Quality & Governance

### Objective
Trust but verify. Learn how to implement **Data Quality** checks using tools like **Great Expectations**. Ensure that your data is not just "there," but that it is accurate, timely, and follows the expected schema, preventing "Silent Failures" where bad data flows into your executive dashboards.

### Core Concepts to Master
- **Expectations:** Assertions about your data (e.g., "The `age` column should never be above 120").
- **Data Profiles:** Automatically generating a summary of a dataset to identify outliers and distributions.
- **Validation Results:** The report generated after comparing a dataset against your expectations.
- **Data Observability:** Monitoring the "Health" of your data over time (e.g., "Is the volume of data today significantly lower than yesterday?").

### Research Topics
- "What is Great Expectations (GX) and how does it work?"
- "Data Quality vs Data Integrity"
- "Implementing 'Data Contracts' in engineering teams"

---

### The Practical Challenge

**Part 1: Defining Expectations**
1. Take a dataset you've worked with previously.
2. Define 3 critical rules:
   - "Column `user_id` should always be unique."
   - "Column `status` should only contain ['Active', 'Pending', 'Closed']."
   - "Column `created_at` should be in the past."

**Part 2: Running a Validation**
1. Use Great Expectations to validate your dataset against these rules.
2. Generate a "Data Docs" report (the HTML dashboard provided by GX).
3. Inspect the report. Identify exactly which rows failed which rule.

**Part 3: The "Statistcal" Check**
1. Research how to check for "Average" or "Standard Deviation."
2. Create an expectation that the "Average Order Value" should be between $10 and $1000.
3. If a bug in the code causes every order to be listed as $0.00, explain how this check would catch the issue even if the schema is perfect.

**Part 4: Data Governance (Conceptual)**
1. Research **Data Lineage** tools like **OpenLineage** or **Amundsen**.
2. Discuss: If you see a wrong number in a Tableau dashboard, how do you trace it back through the Warehouse, dbt models, and Kafka topics to find the original source of the error?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-testing. If you have 500 expectations on every small table, your pipeline will run very slowly. Focus your testing on the "Critical Path" (the data that drives business decisions).
- **Gotcha 2:** Hard-coding Values. Avoid hard-coding specific values that might change (like `expect_column_max_to_be_342`). Use statistical ranges or dynamic thresholds instead.

### Reflection Question
Why is "Bad data" often considered more dangerous than "No data" (a complete system outage)?
