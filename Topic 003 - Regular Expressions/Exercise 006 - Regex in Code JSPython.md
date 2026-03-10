# Exercise 006 - Regex in Code (JS/Python)

### Objective
Integrate regular expressions structurally into a programming language (Python or JavaScript) to match, dynamically extract arrays, and execute programmatic replacements.

### Core Concepts to Master
- **Python `re` module:** Using `re.search()`, `re.findall()`, `re.sub()`.
- **JavaScript `RegExp` object:** Using `string.match()`, `regex.test()`, `string.replace()`.
- **String Escaping in Code:** Understanding why a backslash `\` in Regex often requires a double backslash `\\` when typed inside a programming language string, and how to use Raw Strings to prevent it.

### Research Topics
- "Python re module tutorial and Raw Strings"
- "JavaScript regex methods test vs match"
- "JavaScript String replace with Regex global flag"

---

### The Practical Challenge

**Part 1: The JavaScript Regex API**
1. Create a file `regex_tasks.js`.
2. Define a messy test string: `const text = "Contact admins at jane_doe@email.com or bob123@work-net.org";`
3. Define a regex pattern using JS literal syntax (slashes): `const emailPattern = /[\w.-]+@[\w.-]+\.\w+/g;`
4. Task 1: Check if the string *contains* an email. Log the boolean result using the `.test()` method: `console.log(emailPattern.test(text));`
5. Task 2: Extract an array of all matches structurally string. Log the output using `.match()`: `console.log(text.match(emailPattern));`
6. Run the file using `node regex_tasks.js`.

**Part 2: The Python `re` API**
1. Create a file `regex_tasks.py`.
2. Import the module and define a string:
   ```python
   import re
   text = "The error code is 404 on port 8080."
   ```
3. Use `re.search()` to find the first group of digits. It returns a 'Match Object'. Print it.
4. Use `re.findall(r'\d+', text)` to extract a list of all numbers. Print the resulting list.
   *Notice the `r` before the string natively turns it into a 'Raw String', meaning you don't have to double escape `\\d`!*
5. Run the file using `python3 regex_tasks.py`.

**Part 3: Programmatic Replacement**
1. Jump back to `regex_tasks.js`. Let's build a profanity filter.
2. Define: `const comment = "This app is awful and terrible!";`
3. Define: `const badWords = /awful|terrible/gi;` (The `i` flag ignores case).
4. Use `.replace`: `const clean = comment.replace(badWords, "***");`
5. Log `clean`. It should output: `This app is *** and ***!`.
6. Advanced JS: Pass a function as the second argument to `.replace` to calculate the length of the matched word and return exactly that many asterisks, rather than hardcoding three `***`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** In JavaScript, if you forget the `g` (global) flag on your regex `/pattern/g`, the `.replace` or `.match` method will immediately stop executing after the very first match it finds.
- **Gotcha 2:** In Python, defining a regex string like `"\bword\b"` will fail spectacularly because Python interprets `\b` as a physical Backspace character! Always prefix python regex strings with `r` (raw string), e.g., `r"\bword\b"`.
- **Gotcha 3:** Executing `.test()` repeatedly in JavaScript on a regex initialized with the `g` global flag causes the regex internal cursor (lastIndex) to advance. A second call might falsely return `false` on the same string! Be careful with global state.

### Reflection Question
Fundamentally, Regex is a "Domain Specific Language" (DSL). Why do general-purpose languages like Python and JavaScript depend entirely on calling external Regex C-Libraries rather than looping over strings themselves natively?