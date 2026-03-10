# Exercise 004 - Databases I (SQL Foundations)

### Objective
Move beyond ephemeral in-memory storage. Initialize a relational database (PostgreSQL or SQLite) and master the Structured Query Language (SQL) to define tables and persist data across server restarts.

### Core Concepts to Master
- **Relational Databases (RDBMS):** Systems that store data in rigid tables with predefined columns and types.
- **SQL (Structured Query Language):** The universal declarative language used to communicate with relational data.
- **DDL (Data Definition Language):** SQL commands used to create and modify the structure itself (`CREATE TABLE`, `ALTER`).
- **Data Types:** Understanding the storage difference between `VARCHAR`, `INTEGER`, `BOOLEAN`, and `TIMESTAMP`.

### Research Topics
- "Basic SQL syntax for beginners"
- "SQL vs NoSQL which one to choose"
- "Installing SQLite on local machine"

---

### The Practical Challenge

**Part 1: The First Table**
1. Install a lightweight SQL engine like SQLite for local development.
2. Create a new database file named `blog.db`.
3. Write your first "Schema" script to define a `users` table:
   ```sql
   CREATE TABLE users (
       id INTEGER PRIMARY KEY AUTOINCREMENT,
       username TEXT NOT NULL UNIQUE,
       email TEXT NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```
4. Execute this command via your SQL CLI or a GUI tool (like DB Browser for SQLite).

**Part 2: Manual Data Insertion**
1. Learn the `INSERT` command to add rows to your table.
2. Draft a query to add three unique users:
   `INSERT INTO users (username, email) VALUES ('alice', 'alice@example.com');`
3. Notice that you do not need to provide an `id` or `created_at` value; the database handles these automatically based on your schema definition.

**Part 3: The Query Pipeline**
1. Master the `SELECT` statement to retrieve data.
2. Write queries to:
   - Fetch all users.
   - Fetch only the `username` column from the table.
   - Fetch any user where the username is exactly 'alice' (using `WHERE`).
3. Observe how SQL allows you to surgically filter data without downloading the entire dataset.

**Part 4: Altering and Dropping**
1. In reality, requirements change.
2. Use the `ALTER TABLE` command to add a new column `bio` (type TEXT) to your users table.
3. Update specific records using `UPDATE`:
   `UPDATE users SET bio = 'Learning SQL!' WHERE username = 'alice';`
4. Finally, practice the "Nuclear Option." Use `DROP TABLE users;` to completely delete the data and structure. This confirms you understand the finality of DDL operations.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Semicolons. In SQL, a command is not executed until it sees a `;`. If your CLI is stuck and not responding, you likely forgot the closing semicolon.
- **Gotcha 2:** String Quotes. In standard SQL, strings must be wrapped in single quotes `'text'`. Double quotes `"text"` are typically reserved for identifying database objects like table or column names.

### Reflection Question
Why are relational databases considered "strongly typed" compared to storing data in a flexible JSON file on your local disk?