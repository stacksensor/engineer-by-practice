# Exercise 006 - Databases III (ORM - Sequelize/Prisma)

### Objective
Graduate from raw SQL strings. Implement an Object-Relational Mapper (ORM) to interact with your database using native JavaScript objects and promises, reducing the risk of SQL injection and improving developer speed.

### Core Concepts to Master
- **ORM (Object-Relational Mapping):** A library that abstracts database tables into JavaScript Classes and rows into Instances.
- **Models:** Defining the structure of your data inside your JavaScript code (Mirroring the SQL Schema).
- **Synchronous Syncing:** Allowing the ORM to automatically create or update SQL tables based on your JS Model definitions.
- **Migrations:** Version-control for your database schema, allowing teams to roll back changes safely.

### Research Topics
- "Prisma vs Sequelize for Node.js"
- "Benefits of using an ORM"
- "Understanding database migrations"

---

### The Practical Challenge

**Part 1: The ORM Setup**
1. Choose a popular ORM (e.g., Sequelize or Prisma). For this exercise, assume Sequelize.
2. Install the library: `npm install sequelize sqlite3`.
3. Initialize the connection in a new `db.js` file:
   ```javascript
   const { Sequelize } = require('sequelize');
   const sequelize = new Sequelize({
       dialect: 'sqlite',
       storage: './database.sqlite'
   });
   ```

**Part 2: Model Definition**
1. Define your `User` model natively in JS. This replaces the manual `CREATE TABLE` step:
   ```javascript
   const User = sequelize.define('User', {
       username: Sequelize.STRING,
       email: Sequelize.STRING
   });
   ```
2. Call `await sequelize.sync();` to force the ORM to physically create the `.sqlite` file and the corresponding tables.

**Part 3: The JS CRUD Cycle**
1. Standardize your server logic to use Model methods.
2. Create a user: `await User.create({ username: 'alice', email: 'alice@email.com' });`
3. Find users: `const users = await User.findAll();`
4. Update a user: `await User.update({ username: 'alicia' }, { where: { id: 1 } });`
5. Note how you are interacting with familiar JS objects rather than complex SQL strings.

**Part 4: Handling Associations**
1. Define the relationship between `User` and `Article` models in JS.
2. Use the ORM's association methods:
   `User.hasMany(Article);`
   `Article.belongsTo(User);`
3. Re-sync the database. Check the SQL schema (using a GUI tool). Notice that the ORM automatically added a `UserId` foreign key to the `articles` table without you explicitly writing it.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-syncing. Using `{ force: true }` in your `sync()` function will drop and recreate your tables every time the server restarts, wiping all your local data. Use this only in development.
- **Gotcha 2:** Naming Conventions. ORMs often guess table names (e.g., converting `User` to `Users`). If you are connecting to an existing database, ensure you explicitly define the `tableName` property to prevent "Table not found" errors.

### Reflection Question
What are the trade-offs between writing "Raw SQL" (for performance and control) versus using an "ORM" (for safety and speed)?