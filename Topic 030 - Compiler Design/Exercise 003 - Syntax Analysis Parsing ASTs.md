# Exercise 003 - Syntax Analysis (Parsing) & ASTs

### Objective
Build the tree. Master the second stage of a compiler: **Syntax Analysis (Parsing)**. Learn how to take a flat list of tokens and turn them into a hierarchical **Abstract Syntax Tree (AST)**. Understand the "Rules of Grammer" for a programming language and how to catch "Syntax Errors" (like a missing parenthesis).

### Core Concepts to Master
- **The Parser:** The component that interprets a sequence of tokens based on a set of rules.
- **Context-Free Grammar (CFG):** The set of recursive rules that define a language (e.g., "An `if` statement must be followed by an `expression` and a `block`").
- **Recursive Descent Parsing:** A simple but powerful way to write a parser by creating one function for every "Rule" in your grammar.
- **Abstract Syntax Tree (AST):** A tree representation of the structure of code (e.g., the `+` is the parent of its two `operands`).

### Research Topics
- "Recursive Descent Parsing for beginners"
- "What is an AST (Abstract Syntax Tree)?"
- "Visually exploring ASTs: AST Explorer (online tool)"
- "Parsing expressions: Precedence and Associativity"

---

### The Practical Challenge

**Part 1: The Visual Tree**
1. Use an online tool like **AST Explorer**.
2. Type a simple function in JavaScript or Python.
3. Observe the "Tree" structure. Locate the `FunctionDeclaration`, the `Param`, and the `Body`.
4. Discuss: How is this representation easier for a computer to process than a raw string of text?

**Part 2: Precedence Logic**
1. Look at the expression `2 + 3 * 4`.
2. Draw two possible trees:
   - Tree A: `+` at the root, with `2` and `(3 * 4)` as children.
   - Tree B: `*` at the root, with `(2 + 3)` and `4` as children.
3. Discuss: Which tree is correct according to standard math? How does a Parser "Know" to create Tree A?

**Part 3: Missing Parenthesis (Error Handling)**
1. In a Recursive Descent Parser, if a function expects a `)` but sees a `;`, it throws a "Syntax Error."
2. Imagine you are writing the code for this parser. 
3. Write an error message that helps the user: "Expected ')' at line 5, column 10." 
4. Discuss: Why is a "Friendly" error message better than just "Syntax Error"?

**Part 4: Parser Generators (Conceptual)**
1. Research tools like **ANTLR**, **Bison**, or **Yacc**.
2. These tools take a "Grammar File" (defining the rules) and "Auto-generate" the parser code.
3. Discuss the trade-off: Hand-written parsers (like in the Go compiler) vs. Generated parsers.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Infinite Recursion. If a rule says "An Expression is an Expression followed by a +," the parser will call itself forever. This is called "Left Recursion" and must be fixed.
- **Gotcha 2:** Ambiguous Grammar. If a rule can be interpreted in two different ways, the parser won't know which tree to build.

### Reflection Question
Why is the "Syntax Analysis" phase responsible for checking if you missed a parenthesis, but NOT responsible for checking if you added a string to an integer? (Hint: See the next exercise!).
