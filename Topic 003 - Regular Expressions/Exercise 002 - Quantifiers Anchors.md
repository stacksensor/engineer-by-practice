# Exercise 002 - Quantifiers & Anchors

### Objective
Control how many consecutive times a character or pattern appears, and securely tie expressions to the absolute start or absolute end of a line for strict validation.

### Core Concepts to Master
- **Quantifiers:** Specify how many instances of a preceding item must be present:
  - `*`: 0 or more times.
  - `+`: 1 or more times.
  - `?`: 0 or 1 time (optional).
  - `{n,m}`: Between n and m times strictly.
- **Greedy vs. Lazy Matching:** By default, regex modifiers take as much text as mathematically possible (Greedy). Adding a `?` after a quantifier forces it to match as little as possible (Lazy).
- **line Anchors (`^`, `$`):** Instead of matching physical characters, these match an invisible position (the absolute start of a string or absolute end of a string).

### Research Topics
- "Regex quantifiers (*, +, ?, {}) explained"
- "Regex greedy vs lazy matching examples HTML tags"
- "Regex start and end of string anchors ^ and $"

---

### The Practical Challenge

**Part 1: Strict Width Quantifiers**
1. Open Regex101.com. Put several test lines in the text area:
   `Phone: 123-456-7890`
   `Phone: 12-456-7890`
   `Phone: 123-45-78909`
2. Write a regex using the explicit `{n}` quantifier combined with the digit shorthand `\d` to match ONLY the correctly formatted US phone number line.
   Example pattern: `\d{3}-\d{3}-\d{4}`. Notice how it strictly rejects the other two lines.
3. Change `{n}` to a range `{n,m}`. Try `\d{2,3}` and observe what highlights.

**Part 2: Optional and Infinite Quantifiers**
1. Clear the input. Type: `color colour colur`.
2. Write a pattern `colou?r`. The `?` makes the `u` optional. Observe it matching both the American (`color`) and British (`colour`) spellings, while completely ignoring `colur`.
3. Type out a wildly formatted log file segment: `Error: 404`, `Error:    500`, `Error:502`.
4. Use the `*` (zero or more) and `+` (one or more) with the whitespace shorthand `\s`.
   Type `Error:\s*\d{3}`. Notice how the `*` seamlessly spans 0 spaces, 1 space, or 10 spaces to grab the error code.

**Part 3: The Greedy vs Lazy Trap**
1. Clear the inputs. Paste some HTML string into the test area: 
   `<div>Hello</div> and <div>World</div>`
2. Type a greedy regex to try and grab the first element: `<div>.*</div>`.
   *(`.` means any character, `*` means zero or more times).*
3. Observe what highlights. It grabs everything from the very first `<` to the absolute last `>`, highlighting the entire line as one giant match. This is the "Greedy" default.
4. Fix it using the Lazy modifier. Type `<div>.*?</div>`.
5. Notice how it now stops immediately at the *first* closing `</div>`, generating two separate, accurate matches!

**Part 4: Anchoring Strings for Validation**
1. Clear the test string. Type:
   `12345`
   `my zip is 12345`
   `1234567`
2. Assume you are validating a strict web form input that must be EXACTLY a 5 digit zip code, nothing else.
3. Try typing `\d{5}`. Notice it frustratingly grabs `12345` out of the middle of the sentence, and grabs the first 5 digits of `1234567`. If this was form validation, it would falsely pass incorrect data!
4. Wrap your pattern in Anchors. Type `^\d{5}$` (`^` means start of line, `$` means end of line).
5. Suddenly, it strictly matches only the first line (`12345`) and completely ignores the others, making it safe for database validation.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Greedy matching on HTML or markdown tags (`<.*>`) is the number one cause of horrific bugs for beginners parsing strings. Always consider `.*?` when pulling text sandwiched between tags.
- **Gotcha 2:** Without the anchors `^` and `$`, a pattern like `\d{3}` will return a perfectly valid match even if it's sitting illegally inside a block of text like `abc123def`. Form validations almost *always* require anchors.
- **Gotcha 3:** Be careful with the `*` quantifier. Because it means "Zero or more", `A*` technically successfully matches a blank space or an entirely unrelated string (returning a zero-width match).

### Reflection Question
In web development, when registering a new user, you check if the `username` input matches `^[a-zA-Z0-9_]{3,16}$`. Why are the `^` and `$` absolutely critical here? What malicious input might pass validation if you forgot them?