# Exercise 002 - Vector Graphics

### Objective
Abandon pixel matrices entirely. Master the mathematical precision of Scalable Vector Graphics (SVG), formatting images as explicit geometric formulas so they can scale to the size of a billboard with zero pixelation and fractional file sizes.

### Core Concepts to Master
- **Vector Mathematics:** Unlike raster photos (pixels), vectors are rendered using XY coordinate graphs. A line is just `Start(0,0)` to `End(100,100)`.
- **SVG Architecture:** The underlying XML markup language defining native vector algorithms for the web browser natively.
- **Paths and Polygons:** Complex structural nodes combining curves, arcs, and rigid boundaries.
- **Infinite Scalability:** An SVG mathematically recalculates its geometry dynamically upon resize, ensuring edges are permanently perfectly sharp regardless of monitor resolution.

### Research Topics
- "Raster vs Vector graphics web design"
- "HTML SVG tutorial basics"
- "Understanding SVG paths and viewBox"

---

### The Practical Challenge

**Part 1: The Raw Coordinate Grid**
1. Open a blank HTML file. Forget `<img>` tags. Inject raw structural math directly inside the `<body>`:
   ```html
   <svg width="200" height="200" style="border: 2px solid black;">
       <circle cx="100" cy="100" r="50" fill="red" />
   </svg>
   ```
2. The `<circle>` is centered at X:`100`, Y:`100` natively. The radius `r` is `50` pixels.
3. Open it mathematically in your browser. Verify the precise red dot.
4. Try injecting another native element natively: 
   `<rect x="10" y="10" width="50" height="50" fill="blue" />`
5. The rectangle natively spawns at the exact XY structural coordinate graph natively.

**Part 2: The ViewBox Concept**
1. `width` and `height` dictate the physical box on the webpage perfectly. 
2. The `viewBox="min-x min-y width height"` attribute defines the internal mathematical coordinate space natively.
3. Replace the `width` and `height` entirely:
   `<svg viewBox="0 0 100 100" style="border: 2px solid green; width: 400px; height: 400px;">`
4. The internal circle is now massive! You configured an internal mathematical grid natively of 100x100 pixels completely, then instructed the browser to stretch that flawless math over a physical 400x400 physical space natively.

**Part 3: The Omnipotent <path> Element**
1. All shapes (circles, rects) mathematically compile down to native `<path>` tags structurally. Paths are instructions for a robotic drawing pen completely.
2. Build an explicit path mapping:
   `<path d="M 50 50 L 150 50 L 100 150 Z" fill="orange" />`
3. Decode the letters mathematically:
   - `M 50 50`: "Move the pen to X50/Y50 without drawing".
   - `L 150 50`: "Draw a straight Line to X150/Y50".
   - `L 100 150`: "Draw a Line down to X100/Y150".
   - `Z`: "Close the path organically back to the Starting Point".
4. You successfully manually programmed a precise mathematical triangle struct natively.

**Part 4: Styling SVG with CSS**
1. Because SVGs are native HTML Document Nodes strictly, they securely obey organic external CSS heavily.
2. Add a `class="pulse"` to your triangle structure directly.
3. Implement a CSS keyframe smoothly perfectly targeting `<path>` mathematically natively:
   ```css
   .pulse {
       transition: fill 0.3s ease;
   }
   .pulse:hover {
       fill: purple;
       transform: scale(1.1);
   }
   ```
4. Note that SVGs use `fill` and `stroke` instead of generic `background-color` and `border` structurally.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** A `Z-index` algorithm rule does not mathematically exist inside the SVG coordinate grid natively. Shapes overlapping structurally are exclusively layered rigidly based strictly on their physical top-to-bottom sequence precisely inside the HTML markup explicitly.
- **Gotcha 2:** Junior designers often mistakenly attempt to export complex highly-detailed photographs as SVG formats entirely. SVG is structurally incapable of efficiently encoding millions of unique pixel gradient structures natively. It will generate a crashing 50MB mathematical XML file algorithmically.

### Reflection Question
Why are modern professional web icons mathematically universally built natively using SVG instead of standard PNG images mathematically, and what precise impact does this have completely on loading multiple distinct hover-state colors perfectly?