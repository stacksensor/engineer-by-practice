# Exercise 004 - Semantic Analysis & Type Systems

### Objective
Check for meaning. Master **Semantic Analysis**, the third stage of a compiler. Learn how the compiler ensures that the code "Makes Sense"—checking that variables are declared before use, that types match (e.g., no adding "hello" to 5), and that functions are called with the right number of arguments.

### Core Concepts to Master
- **Symbol Table:** A data structure (usually a Hash Map) that stores all the variables and functions and their types as the compiler moves through the code.
- **Scope:** Determining which variables are visible in which part of the code (Local vs Global).
- **Type Checking:** 
  - **Static Typing:** Checking types at compile time (C++, Rust).
  - **Dynamic Typing:** Checking types at runtime (Python, JS).
- **Type Inference:** How the compiler "Guesses" the type of a variable (`let x = 5` implies x is an integer) without the user saying it.

### Research Topics
- "What is a Symbol Table in a compiler?"
- "Static vs Dynamic Type Checking"
- "Semantic Analysis: Identifier resolution and type inference"

---

### The Practical Challenge

**Part 1: The Symbol Table Lab**
1. Read this code:
   ```
   var x = 10;
   func foo(y) {
     var z = 20;
     print(x + y + z);
   }
   ```
2. Draw the Symbol Table for the `foo` function. 
3. Include the Variable Name, the Type, and its "Scope" (Global vs Local).
4. Discuss: When the compiler reaches `print(x)`, how does it "Look up" that x is a global variable?

**Part 2: Finding a Semantic Error**
1. Which of these is a **Syntax Error** (the tree can't be built) and which is a **Semantic Error** (the tree builds, but it's nonsense)?
   - `if (x == 10) {` (Missing closing brace).
   - `var name = "Alex"; var age = name + 10;`
2. Discuss why the compiler needs to "Annotate" the AST with type information to catch the second error.

**Part 3: Type Systems Comparison**
1. Research **TypeScript**. 
2. Discuss: TypeScript doesn't change how JavaScript *runs*; it just adds a "Semantic Analysis" layer *before* the code runs. 
3. How does this help a developer avoid "Undefined is not a function" errors?

**Part 4: Declaration Checks**
1. Research why languages like C++ or Go require you to declare a variable before using it. 
2. Discuss the security and performance benefits of "Knowing" every variable's size and location before execution begins.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Name Shadows. If you have a local variable `x` and a global variable `x`, which one does the compiler pick? (Usually the "closest" scope wins).
- **Gotcha 2:** The "Any" escape. In some languages, you can tell the compiler "Trust me, I'm a professional, don't check the type." This is where bugs hide.

### Reflection Question
Why is a language with "Static Typing" considered safer for large-scale engineering teams than one with "Dynamic Typing"?
