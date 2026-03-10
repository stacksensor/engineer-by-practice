# Exercise 005 - Databases II (Relationships)

### Objective
Master data connectivity. Expand your schema to include multiple tables and implement Foreign Keys to establish relationships between data (e.g., Users owning Articles).

### Core Concepts to Master
- **Foreign Keys:** A column in one table that points to the Primary Key of another table, creating a logical link.
- **One-to-Many Relationships:** A single parent record (User) having multiple child records (Articles).
- **JOINS:** SQL statements that allow you to combine rows from multiple tables based on a related column.
- **Referential Integrity:** Rules that prevent you from deleting a User if they still have active Articles linked to them.

### Research Topics
- "SQL One to Many relationship tutorial"
- "Inner Join vs Left Join explained"
- "Entity Relationship Diagrams (ERD) basics"

---

### The Practical Challenge

**Part 1: The Article Schema**
1. Create a second table named `articles`.
2. Link it back to the `users` table created in the previous exercise using a `user_id` column:
   ```sql
   CREATE TABLE articles (
       id INTEGER PRIMARY KEY AUTOINCREMENT,
       title TEXT NOT NULL,
       content TEXT,
       user_id INTEGER,
       FOREIGN KEY (user_id) REFERENCES users(id)
   );
   ```
3. Execute the command and verify both tables exist in your database.

**Part 2: Inserting Relational Data**
1. Insert two articles into the database.
2. You must manually provide the `user_id` for an existing user (e.g., if Alice is ID 1, use `1` as the `user_id`).
   `INSERT INTO articles (title, content, user_id) VALUES ('My First Post', 'Hello world!', 1);`
3. Attempt to insert an article with a `user_id` that does not exist (e.g., 999). Note if your database engine blocks this (SQLite requires `PRAGMA foreign_keys = ON;` to enforce this check).

**Part 3: The INNER JOIN**
1. Fetch all articles along with their author's username.
2. Use the `JOIN` syntax to merge the tables:
   ```sql
   SELECT articles.title, users.username 
   FROM articles
   JOIN users ON articles.user_id = users.id;
   ```
3. Observe how the database engine performs the lookup and returns a unified combined row.

**Part 4: The LEFT JOIN**
1. What if a user has no articles?
2. Run a `SELECT * FROM users JOIN articles...` query. Notice that users without articles disappear from the results.
3. Replace `JOIN` with `LEFT JOIN`. 
4. Observe how all users are now listed, and the article columns return `NULL` for those who haven't posted yet. This is a critical distinction in relational reporting.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Column Name Collisions. If both tables have an `id` column, simply selecting `id` in a JOIN will cause an error or overwrite. Always use dot notation (`users.id`, `articles.id`) or aliases (`AS user_id`) in your SELECT queries.
- **Gotcha 2:** Enforcing Foreign Keys. In SQLite, foreign key constraints are often disabled by default for backward compatibility. Always run `PRAGMA foreign_keys = ON;` when you connect to ensure your data stays consistent.

### Reflection Question
How do relational Foreign Keys provide better data security than simply storing a "username" string inside your articles table?