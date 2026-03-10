# Exercise 001 - Regex Basics

### Objective
Understand the foundational building blocks of Regular Expressions (Regex) for finding intricate text patterns in strings. Move beyond simple "Find and Replace" literal searches.

### Core Concepts to Master
- **Regular Expressions (Regex / PCRE):** A sequence of characters specifying a search pattern in text. Used across almost all programming languages and text editors.
- **Literal Characters vs. Metacharacters:** 
  - Literal: Finding the exact letter `a` or number `1`.
  - Metacharacters: Characters that have special programmatic meaning, like `.` (match any character) or `*` (match 0 or more).
- **Character Classes (`[]`):** Matching any one character out of a specifically defined set of characters, like `[abc]` matching either a, b, or c.
- **Shorthand Classes:** Built-in shortcuts for common patterns like `\d` (digit), `\w` (word character), and `\s` (whitespace).

### Research Topics
- "Introduction to Regular Expressions"
- "Regex character classes and ranges"
- "Escaping special characters in Regex"
- "Regex \d vs \w vs \s"

---

### The Practical Challenge

**Part 1: Literal and Metacharacter Fundamentals**
1. Open an interactive visual regex tester in your browser, like Regex101.com. Ensure the "Flavor" on the left panel is set to PCRE or JavaScript.
2. In the "Test String" area, type: `cat bat rat mat hat flat splat`.
3. In the "Regular Expression" input at the top, type `at`. Notice how it highlights every instance of `at` across all the words.
4. Next, use the "Any Character" metacharacter (`.`). Type `.at`. Observe how it matches `cat`, `bat`, `rat`, `mat`, and `hat` perfectly, but for `flat` it only matches `lat`, and for `splat` it only matches `lat`!

**Part 2: Character Classes**
1. Clear the regex input at the top.
2. Write a regex using a character class `[...]` to match ONLY `cat`, `bat`, and `rat`. Your regex should look something like `[cbr]at`. Notice how it completely ignores `mat` and `hat`.
3. Modify your character class to use a range. If you want any lower case letter from `a` to `m`, use `[a-m]at`. Observe which words are now highlighted in the test string.
4. Combine ranges to allow uppercase characters: `[a-mA-M]at`.

**Part 3: Inverting Logic and Escaping**
1. Invert the character class using the caret symbol `^` inside the brackets. Type `[^cbr]at`. Notice how it now highlights the `mat` and `hat`, explicitly avoiding `cat`, `bat`, and `rat`.
2. Clear the test string and type: `File name: document.txt. Size: 14MB.`
3. Try to match the literal `.txt` by typing `.txt`. Notice it matches `etxt` or ` itxt` if you type them! The dot `.` is a wildcard metacharacter.
4. Escape the dot using a backslash to force it to act as a literal character: `\.txt`. Now it only highlights the file extension.

**Part 4: Shorthand Classes**
1. Clear the test text and paste a randomized block containing dates, times, and phone numbers:
   `Date: 2023-10-24, Event: 1, Contact: 555-0199`
2. Extract the numbers. Instead of typing `[0-9]`, use the shorthand `\d` (digit). Type `\d`. Observe it capturing individual numbers.
3. Use the capital version `\D` (NOT digit). Notice how it highlights every letter, space, and punctuation mark, ignoring the numbers.
4. Use `\w` (Word Character: alphanumeric plus underscore) and `\W` (Not word character) to isolate the punctuation and spaces. Use `\s` to isolate only the spaces.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Forgetting to escape a metacharacter when you mean it literally. If you are trying to find where a sentence ends and you type `.` instead of `\.`, the engine matches literally every character in the document instead of the period.
- **Gotcha 2:** Whitespace matters strictly in regex. `[a-z] at` expects a specifically defined space character between the letter and the word `at`. Do not space out your regex lines unless using the specific extended format flag (`/x`).
- **Gotcha 3:** Case sensitivity is on by default. `[A-Z]` will ignore lowercase letters unless you turn on the `i` (Ignore Case) flag in the Regex101 settings or your editor's search bar.

### Reflection Question
Why do programming languages often require you to use double backslashes (like `\\d`) when defining a Regular Expression inside a string variable?