# Exercise 003 - CSS Selectors & Specificity

### Objective
Master how browsers calculate priority when two CSS rules clash, and learn how to target complex relative DOM elements without adding hundreds of specific classes to your HTML document.

### Core Concepts to Master
- **The Cascade:** CSS stands for Cascading Style Sheets. Rules defined lower perfectly down in the file overwrite conflicting rules defined higher up.
- **Specificity Weight Calculation:** Elements are ranked. `tag` < `class` < `ID` < `inline-style` < `!important`.
- **Combinators:** Targeting relationships (`>` direct child, ` ` descendant, `+` adjacent sibling, `~` general sibling).
- **Pseudo-classes:** Styling states (`:hover`, `:active`, `:first-child`, `:nth-child`).

### Research Topics
- "CSS Specificity Wars explained"
- "CSS Descendant vs Direct Child selector"
- "CSS pseudo-classes nth-child formulas"

---

### The Practical Challenge

**Part 1: The Specificity Point System**
1. Create a simple `index.html` file and an adjacent `style.css`. Link them together using `<link rel="stylesheet" href="style.css">` inside your `<head>`.
2. Draw a button: `<button class="primary-btn" id="submit-btn">Click Me</button>`.
3. In `style.css`, create three targeting rules, all attempting to change the background to a different color:
   ```css
   button { background-color: red; }
   .primary-btn { background-color: blue; }
   #submit-btn { background-color: green; }
   ```
4. Load the page. Observe the button is green. 
   *(Logic: IDs are infinitely more specific than classes. Classes are infinitely more specific than tags).*
5. Add an inline style exactly in your HTML: `<button ... style="background-color: orange;">`. Notice the button turns orange. (Inline beats ID).
6. Go back to your `.primary-btn` class in the CSS file and add `!important`, e.g., `background-color: blue !important;`. The button turns blue. (`!important` beats everything in the universe).

**Part 2: Relationship Combinators**
1. Draw nested structures:
   ```html
   <ul class="nav">
       <li><a href="#">Home</a></li>
       <li><span><a href="#">About</a></span></li>
   </ul>
   ```
2. Target links absolutely anywhere inside the nav (Descendant: space):
   `.nav a { color: red; }` - Notice both links turn red.
3. Change it to target ONLY direct children of `li` elements (Child: `>`):
   `li > a { color: blue; }` - Notice 'Home' turns blue, but 'About' stays red because it's technically a direct child of a `<span>`.

**Part 3: Advanced Pseudo-Classes**
1. Build an unstyled data table or an unordered list with exactly 10 items.
2. Use the `:nth-child()` pseudo-class to create a "Zebra Striped" styling pattern by applying a grey background exclusively to the EVEN rows, skipping the ODD ones.
   `li:nth-child(even) { background-color: #eee; }`
3. Try experimenting with formulas. Apply a border to every 3rd element:
   `li:nth-child(3n) { border: 1px solid black; }`
4. Add a `:hover` state to the list items that instantly changes the text color when your mouse passes over them. Add `:first-child` and `:last-child` styling.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Relying heavily on `#ID` tags for styling traps you. Once you style an element via ID, you can *never* override that color using a `.class` rule somewhere else later. Best practice is to construct 100% of your structural CSS using Classes exclusively.
- **Gotcha 2:** The `!important` tag behaves like a sledgehammer. Adding it to fix a minor bug escalates the specificity war, meaning later when you want to write a media query for mobile screens, you have to use *another* `!important` to override it. Avoid it unless fighting injected 3rd-party library styles.
- **Gotcha 3:** Be careful distinguishing between `:nth-child` and `:nth-of-type`. If you have a `<h1>` followed by three `<p>` tags inside a div, `p:nth-child(1)` targets nothing! (Because the first child is the `h1`).

### Reflection Question
If you have a complex specific CSS rule: `body div.container header nav ul li p.active { color: pink; }`, why is it considered significantly better industry practice to just attach a new class `<p class="nav-active-text">` to the HTML tag and style that directly instead?