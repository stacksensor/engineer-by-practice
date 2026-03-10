# Exercise 004 - Modern Layouts I (Flexbox)

### Objective
Stop relying on outdated `float` and `table` hacks. Master constructing responsive, 1-dimensional layouts (working either strictly in a Row, or strictly in a Column) mapping out perfect spacing mathematically without calculating raw pixel margins manually.

### Core Concepts to Master
- **The Flex Container:** Declaring `display: flex;` unlocks all magical properties on the *direct* children of that container.
- **Main Axis vs Cross Axis:** 
  - If `flex-direction` is `row` (default), the Main Axis is Left-to-Right. The Cross Axis is Top-to-Bottom.
  - If `flex-direction` is `column`, it flips.
- **Justify vs Align:**
  - `justify-content` spaces items along the Main Axis.
  - `align-items` aligns items along the Cross Axis.
- **flex-wrap:** Controlling if items aggressively squeeze to fit constraints, or cleanly jump down to form a new line when they run out of width.

### Research Topics
- "A Complete Guide to Flexbox CSS-Tricks" (The holy grail article)
- "CSS Flexbox align-items vs justify-content"
- "How flex-grow and flex-shrink work"

---

### The Practical Challenge

**Part 1: Absolute Centering**
1. For twenty years, centering a div horizontally and vertically in CSS was notoriously difficult. Flexbox makes it an exact 3-line formula.
2. In your HTML, create a `<main>` tag. Treat it like the browser window by forcing it via CSS to take up the full height: `height: 100vh;` and width `width: 100vw;`. Give it a grey background.
3. Put a small `<div class="box">` inside it with fixed height/width.
4. Apply the legendary 3-line Flexbox formula to the `<main>` container:
   ```css
   display: flex;
   justify-content: center;
   align-items: center;
   ```
5. Observe the box perfectly snapping to the dead mathematical center of the screen, regardless of how you resize the browser.

**Part 2: Creating a Navigation Bar**
1. Let's space items out along the *Main Axis*.
2. Create a `<nav class="navbar">` container. Inside it, place a Logo `div`, and a `ul` containing 3 links. 
3. Apply `display: flex;` to the `.navbar`. Notice how the logo and the unordered list suddenly collapse horizontally onto the same line (the raw power of flex rows).
4. Apply `justify-content: space-between;`. The Logo violently snaps to the far left, and the `ul` block snaps to the far right. Perfectly distributed!
5. Now fix the `ul` links. Right now they are stacked vertically. Apply `display: flex;` specifically to the `ul` to turn it into a secondary, nested flex container! Add `gap: 20px;` to put clean spacing exclusively between the links.

**Part 3: The Wrapping Card Grid**
1. Create a deeply nested layout: A `<section class="cards-container">` containing six duplicate `<div class="card">` elements.
2. Give all cards a fixed width of `300px` and a height of `200px` with a distinct border.
3. Set `.cards-container { display: flex; }`.
4. Observe the flaw: If the browser is 1000px wide, 6 cards (1800px total width) cannot fit. Flexbox aggressively shrinks them, distorting their proportions.
5. Fix the distortion by commanding Flexbox to wrap: `.cards-container { flex-wrap: wrap; }`. Watch the cards jump to form clean rows mathematically!
6. Add `gap: 15px;` and `justify-content: center;`. You now have a production-ready, highly responsive image gallery.

**Part 4: Flex Grow and Shrink**
1. Create a single full-width row with three colored columns: Left Sidebar, Main Content, Right Sidebar.
2. Set `display: flex` on their parent row container.
3. Instead of defining raw widths (`width: 30%`), apply the `flex` shorthand property securely on the *children*.
4. Give both Sidebars `flex: 1;`. Give the Main Content `flex: 3;`.
5. Flexbox mathematically slices the row into fifths (1+3+1 = 5 parts). It assigns 20% to each sidebar, and 60% perfectly to the main content. Resize the window and watch it recalculate mathematically.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Remembering which axis is which depending on `flex-direction: column`. If your container is a column, `justify-content` now applies vertically, separating blocks top-to-bottom.
- **Gotcha 2:** The `gap` property is relatively new for Flexbox (it started in Grid). It places clean spacing *between* items, but avoids slamming exterior margins against the edge of the container holding them. Use `gap` instead of complex `margin-right: 15px` logic on list items.
- **Gotcha 3:** Applying `flex` layout properties (like `justify-content`) directly onto a child box does nothing. You mandate the layout behavior by applying it strictly to the parent *container* holding the child box.

### Reflection Question
If Flexbox elegantly solves building navigation bars, sidebars, and rows of cards, why did the web community spend years developing `CSS Grid` as a completely separate layout system entirely?