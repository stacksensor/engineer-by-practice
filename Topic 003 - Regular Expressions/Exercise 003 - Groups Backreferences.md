# Exercise 003 - Groups & Backreferences

### Objective
Extract precise pieces of text and reference them internally within your regex or use them to restructure and replace strings natively.

### Core Concepts to Master
- **Capturing Groups `()`:** Groups multiple tokens together mathematically and "captures" the resulting text match into memory for later use (either for extraction or for find-and-replace text restructuring).
- **Non-Capturing Groups `(?:)`:** Groups tokens for logical operations (like checking a quantifier against a whole word) without wasting RAM to save the result.
- **Backreferences (`\1`, `\2`):** Referring back to a previously captured group later in the exact same regex pattern to ensure identical matches.

### Research Topics
- "Regex capturing groups tutorial"
- "Regex non-capturing groups (?:...)"
- "Regex backreferences example"
- "Regex Find and Replace using $1 $2 variables"

---

### The Practical Challenge

**Part 1: Basic Capturing**
1. Open Regex101. Put the following test data in:
   `John Doe, Apples`
   `Jane Smith, Bananas`
   `Bob Bob, Oranges`
2. Write a regex to match the lines without capturing anything: `\w+ \w+, \w+`. It matches the whole line.
3. Now, wrap the First Name in parentheses, and the Last Name in parentheses: `(\w+) (\w+), \w+`.
4. Look at the "Match Information" panel on the right side of Regex101. You will see Group 1 perfectly extracted the first name (`John`), and Group 2 extracted the last name (`Doe`), stripped away from the comma and fruit.

**Part 2: Restructuring with Replacements**
1. Ensure the leftmost UI panel in Regex101 has "Substitution" or "Replacement" enabled.
2. In the "Substitution" input box at the bottom, type: `$2, $1 likes Apples.` (Some engines use `\1` instead of `$1`).
3. View the Result panel. You have completely restructured the string natively from `John Doe, Apples` directly into `Doe, John likes Apples.` without writing a single line of Python or JavaScript logic!
4. Modify the substitution string to try outputting XML formatting: `<lastName>$2</lastName>, <firstName>$1</firstName>`.

**Part 3: Internal Backreferences**
1. Clear the inputs. We now want to find people whose First Name and Last Name are identical (e.g. `Bob Bob`).
2. You cannot just type `\w+ \w+` because that matches `John Doe`.
3. Wrap the first name in a group: `(\w+)`.
4. Add a space, then use a backreference `\1` to command Regex to "Match whatever exact string is held in Group 1".
5. Type `(\w+) \1`. Observe the test lines. It will perfectly highlight `Bob Bob` and ignore `John Doe`!
6. Try pasting the string `The the cat jumped over the the box.` and use a backreference to isolate duplicate words efficiently.

**Part 4: Non-Capturing Groups**
1. Let's say you want to match the word `ha` repeated anywhere from 1 to 3 times (e.g., `ha`, `haha`, `hahaha`).
2. You wrap it in parenthesis to apply the quantifier to the whole chunk: `(ha){1,3}`.
3. The right panel will complain or show that you are permanently capturing 'ha' into memory Group 1. You don't need to extract 'ha'; you just needed the parenthesis to group the word for the `{1,3}` quantifier.
4. Modify the parenthesis to be non-capturing by adding `?:` at exactly the beginning of the parenthesis.
5. Type `(?:ha){1,3}`. Check the Match Information panel. The text matches, but no unneeded capture groups are created, saving execution matrix time.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Too many standard capturing groups rapidly consumes processing memory and makes the regex significantly harder to read. Use non-capturing groups `(?:)` immediately if you do not specifically need to extract the substring into a variable.
- **Gotcha 2:** Group numbering mathematically counts the physical opening parentheses `(` from left to right. Nested groups can make numbering tricky. `((\w+) (\w+))` means Group 1 is the whole string, Group 2 is the first inner word, Group 3 is the second inner word.
- **Gotcha 3:** A backreference `\1` does not rerun the regex logic (e.g. "find any word again"). It searches for the *exact, literal text* that was found the first time by Group 1.

### Reflection Question
If you are parsing extremely messy log files containing millions of lines into a structured JSON database, why is using capture groups directly in a Regex find/replace operation dramatically faster than executing a JavaScript string `.split(',')` operation natively?