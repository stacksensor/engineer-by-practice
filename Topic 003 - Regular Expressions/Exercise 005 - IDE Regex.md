# Exercise 005 - IDE Regex

### Objective
Integrate regular expressions directly into your Integrated Development Environment (IDE) to execute massive, project-wide code refactoring tasks in seconds.

### Core Concepts to Master
- **Editor Regex Engines:** VS Code (uses Rust's regex engine mostly), IntelliJ (Java), and Sublime Text (PCRE). They all support standard syntax.
- **Find and Replace Grouped Manipulation:** Using `$1`, `$2` capture groups directly within the IDE's UI replace bar.
- **Multiline Searches:** Understanding how `\n` (newline) and `\r` (carriage return) manipulate blocks instead of single lines.

### Research Topics
- "VS Code Regex Search and Replace tutorial"
- "Bulk refactoring with Regex in VS Code"
- "Multiline regex matching in code editors"

---

### The Practical Challenge

**Part 1: Enabling and Testing IDE Regex**
1. Open your code editor (e.g. VS Code). Create a new folder `regex_ide` and open it.
2. Create a file `spaghetti.js` and paste 10 lines of horrible old code:
   ```javascript
   var name = "John";
   var age = 30;
   var data = "Active";
   var system = true;
   ```
3. Open the "Search and Replace" panel (CMD/CTRL + F).
4. **CRITICAL:** Click the `.*` icon inside the search bar to enable Regular Expressions.
5. In the Find box, type `var(.*?)=`. Notice it highlights the declarations.
6. In the Replace box, type `const$1=`. Hit the "Replace All" button. Watch the file seamlessly update to modern syntax!

**Part 2: Reordering Arguments**
1. Add this code to your file:
   ```javascript
   connect(port, host);
   connect(8080, "localhost");
   connect(3000, "127.0.0.1");
   ```
2. You realize the library updated, and `connect` now requires the `host` argument first, and `port` second. Imagine doing this to 5,000 lines of code manually.
3. Write a regex to capture the two arguments into groups.
   Find: `connect\((.*?),\s*(.*?)\);`
4. Use the Replace box to swap the captured elements natively:
   Replace: `connect($2, $1);`
5. Press "Replace All" and observe the magic.

**Part 3: Multiline CSS/HTML Formatting**
1. Make an `index.html` file filled with messy HTML:
   ```html
   <div
      class="header"
   >
   Title
   </div>
   ```
2. You want to compress the opening tag down to a single line.
3. In the Find box, type: `<div\n\s*class="(.*?)"\n\s*>`. Notice how `\n` jumps mathematically across the physical line breaks in the editor!
4. In the Replace box, insert: `<div class="$1">`.
5. Execute the replacement.

**Part 4: Global Project Search**
1. In VS Code, open the global sidebar "Search" tab (CMD/CTRL + Shift + F). Enable Regex (`.*`).
2. Type `console\.log\(.*\);` to find every debug statement spanning the entire project folder.
3. Leave the Replace box completely empty.
4. Hit Replace All. You have just purged every single console.log statement from an entire massive codebase in 3 seconds safely.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** When copying regex patterns you found on StackOverflow directly into VS Code's search bar, you generally do *not* need the opening and closing slashes (`/pattern/g`), you just need the raw pattern (`pattern`).
- **Gotcha 2:** When you toggle Regex `.*` active in the IDE, normal searches for strings containing dots or brackets will suddenly break unless you remember to escape them with backslashes. Disable Regex mode when done refactoring.
- **Gotcha 3:** A greedy `.*` search spanning multiple lines `\n` across 1,000 files in an IDE can sometimes crash the editor's RAM. Use `[^\n]*` or lazy `.*?` modifiers for efficiency.

### Reflection Question
If you change a function name from `fetchData` to `retrieveData`, why is doing a blind global text search for "fetchData" dangerous, and how does using a Regex approach employing word boundaries `\bfetchData\b` solve it?