# Exercise 006 - Orchestration with Airflow / Prefect

### Objective
Coordinate complex workflows. Master the tools that schedule and monitor your data pipelines. Learn how to use **Apache Airflow** (using DAGs defined in Python) or **Prefect** to ensure that if a task fails, it is retried, and subsequent tasks wait for their predecessors to succeed.

### Core Concepts to Master
- **DAG (Directed Acyclic Graph):** A collection of all the tasks you want to run, organized in a way that reflects their relationships and dependencies.
- **Operator:** A template for a single task (e.g., `PythonOperator`, `BashOperator`, `SqlOperator`).
- **Scheduler:** The process that determines *when* a task should run based on its schedule and dependencies.
- **Retries & Backfills:** Automatically re-running failed tasks and running historical tasks if the pipeline was turned off for a period of time.

### Research Topics
- "What is an Airflow DAG and how is it structured?"
- "Airflow vs Prefect vs Dagster: Modern Orchestration"
- "Monitoring task status in the Airflow UI"

---

### The Practical Challenge

**Part 1: Defining the DAG**
1. Install Airflow locally (using Docker or `pip`).
2. Create a Python file `hello_dag.py` in your `dags/` folder.
3. Define a simple DAG that runs every day (`@daily`).
4. Add two tasks: `task_a` (prints "Hello") and `task_b` (prints "World").
5. Set the dependency: `task_a >> task_b`.

**Part 2: Integrating with ETL**
1. Create a DAG that coordinates your ETL work from Exercise 002.
2. Task 1: `Extract` (Fetch data from an API).
3. Task 2: `Load` (Write to database).
4. Task 3: `Transform` (Trigger a dbt run using the `BashOperator`).
5. Verify the full run in the Airflow UI.

**Part 3: Handling Failure**
1. Intentionally make `Task 1` fail (e.g., use a wrong URL).
2. Configure `retries=3` and `retry_delay=5` seconds.
3. Watch the Airflow UI as it automatically attempts to restart the task before finally marking it as "Failed."
4. Observe that `Task 2` and `Task 3` are never started because their predecessor failed.

**Part 4: Slack/Email Alerts**
1. Research "Airflow Callbacks."
2. Define a function that prints "ALARM: DAG FAILED" whenever a task enters the failed state.
3. Discuss why alerting is critical for data engineers who manage hundreds of pipelines.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Heavy Logic in DAG Files. The Airflow scheduler parses your Python files every few seconds. If you put heavy data processing logic (like `df.read_csv`) directly in the DAG file, you will crash the scheduler. Only define the *structure* in the DAG file; put the logic inside the Operators/Python functions.
- **Gotcha 2:** Serialization Errors. If you try to pass a massive dataset between tasks using Airflow's internal communication (XCom), you will hit database size limits. Instead, Task A should write a file to S3, and Task B should read that file.

### Reflection Question
Why are "Cron Jobs" (Exercise 004 in Topic 001) usually insufficient for managing professional data pipelines with dozens of dependencies?
