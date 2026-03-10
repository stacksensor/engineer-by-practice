# Exercise 002 - Lexical Analysis (Scanning)

### Objective
Break down the blocks. Master the first stage of a compiler: **Lexical Analysis (Scanning)**. Learn how to transform a raw string of text (source code) into a sequence of meaningful **Tokens** (like `KEYWORD`, `IDENTIFIER`, `OPERATOR`, `STRING`). Understand how the "Lexer" ignores whitespace and comments while identifying the basic building blocks of a language.

### Core Concepts to Master
- **The Lexer/Scanner:** The component that reads source code character-by-character.
- **Token:** The fundamental unit of a language. 
  - Example: `let x = 10;` -> `[LET, IDENT("x"), ASSIGN, INT(10), SEMICOLON]`.
- **Regular Expressions (Regex):** The primary tool used to define the rules for a token (e.g., "A word starting with a letter is an identifier").
- **Finite Automata:** The theoretical "State Machine" behind how a lexer moves between characters.

### Research Topics
- "What is a Lexer and how does it work?"
- "Building a scanner in Python/JS"
- "Tokens vs Lexemes"
- "Regular languages and scanners"

---

### The Practical Challenge

**Part 1: Defining the Tokens**
1. Imagine a tiny language with:
   - Keywords: `if`, `else`, `print`.
   - Operators: `+`, `-`, `=`.
   - Numbers: `0-9`.
   - Identifiers: Words (e.g., `age`, `name`).
2. List the tokens in this string: `if x = 10 print x`.
3. (Answer: `[IF, IDENT("x"), ASSIGN, NUMBER(10), PRINT, IDENT("x")]`).

**Part 2: The "Whitespace" Eraser**
1. Write a simple script (Pseudocode or Real Code) that iterates through a string.
2. If it sees a space (` `) or a newline (`\n`), it skips it.
3. If it sees a slash (`/`) followed by another slash (`/`), it skips everything until the next newline.
4. Discuss: Why does the Lexer remove this data? Does the computer need to know about your comments to run the code?

**Part 3: Handling Strings**
1. Discuss: How does a Lexer know that a space *inside* a string `"Hello World"` should NOT be ignored?
2. Explain the "State" change: When the Lexer sees a quote (`"`), it switches to "String Mode" until it sees another quote.

**Part 4: The Lexer Generator (Conceptual)**
1. Research tools like **Flex** (C/C++), **Lex** (general), or libraries like **Pygments** (Python).
2. Discuss why developers use "Generators" to build lexers instead of writing a million `if/else` statements manually.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** "Maximal Munch." If your language has `>` and `>=`, and the lexer sees `>`, should it stop? Or should it wait for the next character? (The lexer always tries to match the *longest* possible token).
- **Gotcha 2:** Numbers vs Identifiers. A token like `10var` is often invalid. The lexer must decide if this is one token or two, or an error.

### Reflection Question
Why is the Lexical Analysis phase separated from the "Syntax Analysis" (Parsing) phase? (Hint: Think about speed and simplicity).
