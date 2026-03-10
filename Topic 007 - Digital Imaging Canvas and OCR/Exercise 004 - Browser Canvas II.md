# Exercise 004 - Browser Canvas II

### Objective
Master dynamic rendering and animation loops. Construct a functional event loop capable of moving complex objects across the screen at 60 frames per second to simulate fluid physical motion.

### Core Concepts to Master
- **The Animation Loop:** Using `requestAnimationFrame(callback)` to synchronize your drawing code with the monitor's refresh rate (typically 60Hz or 16.6ms per frame).
- **Clearing the Screen:** Because the canvas permanently overwrites pixels, moving an object requires clearing the entire canvas using `clearRect()` before redrawing the object in its new position.
- **Delta Time:** Understanding how to normalize animation speeds across different hardware refresh rates (e.g., 60Hz vs 144Hz monitors).
- **Collision Mathematics:** Implementing basic logic to detect when a moving object intersects with a boundary or another object.

### Research Topics
- "JavaScript requestAnimationFrame tutorial"
- "HTML5 Canvas clearing screen"
- "Basic 2D collision detection mathematics"
- "Moving an object smoothly HTML5 canvas"

---

### The Practical Challenge

**Part 1: The Main Render Loop**
1. Open a fresh HTML file with a canvas: `<canvas id="sim" width="800" height="600"></canvas>`.
2. Construct the basic loop architecture in JavaScript:
   ```javascript
   const canvas = document.getElementById("sim");
   const ctx = canvas.getContext("2d");

   function gameLoop() {
       // Update logic here...
       // Draw logic here...
       
       requestAnimationFrame(gameLoop);
   }
   
   gameLoop();
   ```
3. Run the code and verify that `gameLoop` is executing continuously by logging a message to the console.

**Part 2: Moving Objects and Clearing**
1. Define a ball object outside the loop:
   `let ball = { x: 50, y: 300, vx: 5 };`
   *(vx represents velocity on the X-axis).*
2. Inside `gameLoop()`, update the ball's position:
   `ball.x += ball.vx;` 
3. Draw the ball as a circle:
   ```javascript
   ctx.fillStyle = "blue";
   ctx.beginPath();
   ctx.arc(ball.x, ball.y, 20, 0, Math.PI * 2);
   ctx.fill();
   ```
4. Run the code. You will see a blue trail stretching across the canvas. This is because the old positions are never erased.
5. Fix this by adding `ctx.clearRect(0, 0, canvas.width, canvas.height);` at the very beginning of the `gameLoop` function.
6. The ball should now appear to glide smoothly across the screen.

**Part 3: Boundary Detection**
1. Prevent the ball from flying off the screen.
2. Inside `gameLoop`, add logic to check if the ball hits the left or right edges:
   ```javascript
   if (ball.x + 20 > canvas.width || ball.x - 20 < 0) {
       ball.vx = ball.vx * -1; // Reverse the velocity
   }
   ```
3. The ball should now bounce back and forth between the two walls.

**Part 4: Interactive Input**
1. Add an event listener to the window to track the mouse position.
2. Update the ball's Y-coordinate to match the mouse's vertical position:
   ```javascript
   window.addEventListener('mousemove', (e) => {
       ball.y = e.clientY;
   });
   ```
3. This creates a simple interactive system where the user controls the vertical alignment of the bouncing object.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Never use `setInterval()` for animations. It ignores the screen's refresh rate and can lead to visual stuttering or "tearing." Always use `requestAnimationFrame`.
- **Gotcha 2:** Avoid performing expensive DOM queries (like `document.querySelector`) inside the animation loop. These operations trigger layout recalculations that will drop your frame rate significantly. Perform all queries once before the loop starts.

### Reflection Question
Under what specific hardware conditions might a `requestAnimationFrame` loop appear to run "faster" or "slower" if the movement logic is not normalized using elapsed time (Delta Time)?