# Exercise 004 - Lookaheads & Lookbehinds

### Objective
Understand Zero-Width Assertions in Regex to verify conditions exist ahead of or behind your cursor without actually capturing those conditions into your final match.

### Core Concepts to Master
- **Positive Lookahead `(?=...)`**: Asserts that what immediately follows the current position in the string matches the pattern, without including it in the match.
- **Negative Lookahead `(?!...)`**: Asserts that what immediately follows the current position does NOT match the pattern.
- **Positive Lookbehind `(?<=...)`**: Asserts that what immediately precedes the current position matches the pattern.
- **Negative Lookbehind `(?<!...)`**: Asserts that what immediately precedes the current position does NOT match the pattern.

### Research Topics
- "Regex Lookahead and Lookbehind tutorial"
- "Regex zero-width assertions explained"
- "How to validate passwords using regex lookaheads"

---

### The Practical Challenge

**Part 1: Basic Lookaheads**
1. Open Regex101.com. Put the test lines:
   `apple pie`
   `apple juice`
   `apple tart`
2. You want to match the word `apple`, but ONLY if it is immediately followed by a space and the word `pie`.
3. Type: `apple(?= pie)`. Notice how `apple` is highlighted on the first line, but the space and `pie` are NOT highlighted. It "looked ahead" to verify they existed, but only matched 'apple'.
4. Try a Negative Lookahead: Type `apple(?! pie)`. Observe how it matches the 'apple' in the juice and tart lines!

**Part 2: Basic Lookbehinds**
1. Clear the test string and paste these prices:
   `$100.00`
   `€50.00`
   `£20.00`
   `10.00`
2. You want to extract the number `100.00`, but ONLY if it is preceded by a dollar sign.
3. Type: `(?<=\$)\d+\.\d{2}`. (Notice we escape the `$` because it's a regex metacharacter).
4. See how only `100.00` is highlighted. The dollar sign is used for the logic, but physically excluded from the captured string.
5. Create a Negative Lookbehind `(?<!\$)\d+\.\d{2}` to capture numbers that do NOT have a dollar sign specifically.

**Part 3: Password Validation Constraints**
1. Lookaheads are famously used to build password validators without writing massive blocks of `if/else` statements in code.
2. Put test strings:
   `weakpass`
   `Strong1Pass`
   `Str0!`
3. We need a regex that ensures a password has:
   - At least 1 capital letter.
   - At least 1 number.
   - Is at least 8 characters long.
4. Using a lookahead, we start at the beginning of the string `^` and look across the whole string `.*` for a capital letter `[A-Z]`. Type this assertion: `^(?=.*[A-Z])`
5. Chain another lookahead logic test immediately after it checking for a number: `(?=.*\d)`
6. Now you have asserted conditions! Finally, run the actual match of 8 characters to the end of the line: `.{8,}$`
7. Combine it all: `^(?=.*[A-Z])(?=.*\d).{8,}$`. Notice how this tightly complex logic perfectly validates only `Strong1Pass` in a single line!

**Part 4: Advanced Combination**
1. Try parsing a comma-separated list: `user,admin,superhero,moderator`.
2. Grab the words entirely, but ONLY if they are NOT `admin`.
3. Use word boundaries `\b` (another zero-width assertion) combined with a negative lookahead comparing the word: `\b(?!admin\b)\w+\b`.
4. Observe how it pulls every single word except `admin` flawlessly.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Lookbehinds must often be fixed-width in some regex engines (like Java or older PCRE). This means `(?<=abc)` is valid, but `(?<=a.*c)` throws an error because the engine cannot determine mathematically how far backward to look.
- **Gotcha 2:** Safari browsers (historically) had horrible support for Regex Lookbehinds natively in JavaScript until recently. Always check compatibility if using lookbehinds purely on the frontend.
- **Gotcha 3:** "Zero-width" is crucial to understand. The regex cursor does not advance through the string when evaluating a lookaround; it checks the condition and stays parked perfectly in place, ready to let the main pattern consume characters.

### Reflection Question
When validating that an entire password string satisfies 5 different complex rules, why do chained Lookaheads at the start of the string `^` make it so easy, rather than trying to write a linear sequential matching pattern?