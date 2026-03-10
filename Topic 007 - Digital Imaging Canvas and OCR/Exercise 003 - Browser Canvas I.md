# Exercise 003 - Browser Canvas I

### Objective
Understand the procedural rendering engine of the HTML5 `<canvas>`. Move beyond DOM nodes and harness JavaScript to draw pixels onto a 2D raster plane at high frame rates.

### Core Concepts to Master
- **The Context API (2D):** `canvas.getContext("2d")` provides the drawing API used to render shapes and images.
- **Procedural Graphics:** The canvas does not maintain a tree of shapes. Drawing an object overwrites the underlying pixel data permanently.
- **The State Machine:** The context acts as a state machine where properties like `fillStyle` must be set before executing a draw command.
- **Coordinate Systems:** The origin (0,0) is at the top-left corner. X increases to the right, and Y increases downward.

### Research Topics
- "MDN basic usage of canvas"
- "Canvas getContext 2d"
- "Drawing shapes with HTML5 canvas"

---

### The Practical Challenge

**Part 1: Initializing the Drawing Surface**
1. Create a raw HTML shell containing a canvas element:
   `<canvas id="gameScreen" width="500" height="500" style="border: 2px solid #ccc;"></canvas>`
2. Create `script.js`. Use the DOM API to get the canvas element.
3. Initialize the 2D rendering context:
   `const ctx = canvas.getContext("2d");`
4. Draw a simple rectangle:
   ```javascript
   ctx.fillStyle = "darkblue";
   ctx.fillRect(100, 100, 200, 150);
   ```
5. You have now painted a blue rectangle at coordinates (100,100) that is 200px wide and 150px tall.

**Part 2: The Path Rendering Pipeline**
1. While rectangles are primitives, complex shapes require paths.
2. Begin a new path:
   `ctx.beginPath();`
3. Move the virtual pen to a starting coordinate:
   `ctx.moveTo(50, 50);`
4. Trace lines to new destinations:
   `ctx.lineTo(250, 200);`
   `ctx.lineTo(50, 200);`
5. Close the path:
   `ctx.closePath();`
6. Set the stroke styles and render the outline:
   `ctx.strokeStyle = "red";`
   `ctx.lineWidth = 5;`
   `ctx.stroke();`

**Part 3: Managing Render State**
1. The canvas maintains global styles across operations.
2. Write a loop to draw a series of squares:
   ```javascript
   for (let i = 0; i < 10; i++) {
       ctx.fillStyle = "orange";
       ctx.fillRect(i * 30, i * 30, 20, 20);
   }
   ```
3. Set `ctx.fillStyle` before starting the loop to observe how it persists.
4. Experiment with `ctx.save()` and `ctx.restore()` to isolate style changes between different drawing segments.

**Part 4: Extracting Pixel Data**
1. You can access raw RGB data directly from the canvas memory.
2. Draw a gradient or complex pattern.
3. Use the `getImageData` method:
   `const imageData = ctx.getImageData(0, 0, 500, 500);`
4. Log `imageData.data` to the console.
5. You will see a large TypedArray containing RGBA values for every pixel on the canvas.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Resizing a canvas with CSS (e.g., `width: 100%`) only stretches the rendered image, resulting in blurriness. To increase resolution, you must set the `width` and `height` attributes directly on the HTML element.
- **Gotcha 2:** The canvas has no memory of individual objects. You cannot bind a click listener to a drawn rectangle. Instead, you must listen for clicks on the canvas itself and calculate if the coordinates intersect with your shape.

### Reflection Question
Why is the Canvas API preferred for high-performance games compared to manipulating thousands of individual DOM elements with CSS?