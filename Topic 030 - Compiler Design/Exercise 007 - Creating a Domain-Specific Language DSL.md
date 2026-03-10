# Exercise 007 - Creating a Domain-Specific Language (DSL)

### Objective
Build your own world. Master the creation of a **Domain-Specific Language (DSL)**. Learn how to design a "Mini-language" that is optimized for a specific task (like configuration, math, or data transformation) and implement a simple Lexer/Parser to execute it. Understand why DSLs make developers 10x more productive in specific domains.

### Core Concepts to Master
- **Internal vs External DSL:**
  - **Internal:** A DSL built using the syntax of another language (like a "Fluent API" in Java or Ruby).
  - **External:** A brand new syntax with its own parser (like **SQL**, **HTML**, or **CSS**).
- **Declarative vs Imperative:** 
  - **Declarative:** Stating "What" you want (SQL: `SELECT name FROM users`).
  - **Imperative:** Stating "How" to do it (Python: `for u in users: list.append(u.name)`).
- **Embedded DSLs (eDSLs):** Integration of a specialized syntax within a general-purpose host.

### Research Topics
- "What is a Domain Specific Language (DSL)?"
- "Building a DSL with Python's 'lark' or 'textX'"
- "Common DSL examples: SQL, Makefile, Gherkin"

---

### The Practical Challenge

**Part 1: Identifying a Domain**
1. Think of a repetitive task: 
   - Example 1: Defining a "Pizza order" (Size, Crust, Toppings).
   - Example 2: Moving a "Robot" (Forward, Turn, Jump).
2. Choose one domain and design a "Mini-syntax" for it.
   - Example: `robot -> move 10, turn 90, jump`.

**Part 2: Designing the Syntax**
1. Write down 5 rules for your language.
2. Example: 
   - Commands must end with a `;`.
   - Distances must be integers.
   - Comments start with `#`.
3. Discuss: Why is this better than writing a 50-item JSON object or 50 function calls?

**Part 3: The "Interpreter" Logic (Conceptual)**
1. How would you "Run" this robot language?
   - Step 1: Lex the tokens (ROBOT, MOVE, INT(10)).
   - Step 2: Parse into a list of "Action" objects.
   - Step 3: Loop through the list and call `physical_robot.move(10)`.

**Part 4: The Trade-off**
1. Research **YAML** and **JSON**. 
2. Discuss: Is a "Config file" a DSL? (Answer: Yes, often a declarative one!).
3. When should you build a "Custom Syntax" instead of just using a standard YAML file? (Hint: When logic or complex relations are required).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-engineering. Don't build a DSL for something that can be solved with a simple Python dictionary. 
- **Gotcha 2:** Poor Tooling. If your DSL doesn't have a "Syntax Highlighter" or "Error messages," developers will hate using it.

### Reflection Question
How do DSLs like **SQL** or **HTML** prove that "Removing features" (like loops/variables) can actually make a language *more* powerful for its specific domain?
