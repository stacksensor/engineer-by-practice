# Exercise 001 - Digital Imaging Basics

### Objective
Understand the foundational architecture of digital images. Learn how bit depth, color models, compression algorithms, and spatial resolution mathematically govern how computers display visual data.

### Core Concepts to Master
- **Raster/Bitmap Images:** Images defined mathematically as an enormous grid of individual colored squares (pixels).
- **Color Models (RGB vs CMYK):** 
  - RGB (Additive): Screens emit light. Combining Red, Green, and Blue light at 100% creates White.
  - CMYK (Subtractive): Printers use ink. Ink absorbs light. Combining Cyan, Magenta, and Yellow ink creates dark, muddy Black (K is added for true Black).
- **Bit Depth:** How much mathematical memory is allocated to a single pixel. A standard 8-bit image allows 256 distinct shades per color channel (R: 256 x G: 256 x B: 256 = 16.7 million total colors).
- **Compression Algorithms (Lossless vs Lossy):** 
  - PNG (Lossless): Exact pixel data is preserved, but file sizes are enormous. Supports transparency.
  - JPEG/JPG (Lossy): Mathematical algorithms aggressively permanently delete invisible spatial frequencies to achieve 90% smaller file sizes, creating distinct "blocky" artifacts dynamically.

### Research Topics
- "RGB vs CMYK color profiles explained"
- "How does JPEG image compression fundamentally work"
- "PNG vs WebP web formats"

---

### The Practical Challenge

**Part 1: The Hexadecimal Matrix**
1. Open a blank HTML file and embed a simple CSS colored box: 
   `<div style="width: 100px; height: 100px; background-color: #FF0000;"></div>`
2. The hexadecimal code `#FF0000` is literal computer math. It is split into three 2-digit channels: `FF` (Red), `00` (Green), `00` (Blue).
3. The letters are Base-16 math. `FF` is the absolute maximum value (255 in standard decimal). 
4. Experiment by altering the CSS explicitly. Change it to `#00FF00` (pure green), `#000000` (pure black, zero light), and `#FFFFFF` (pure white, maximum light).

**Part 2: The Alpha Channel Subsystem**
1. Standard RGB uses 3 channels. Modern digital imaging adds a 4th mathematical channel explicitly: Alpha (Transparency).
2. Change your CSS explicitly to use the `rgba()` syntax:
   `background-color: rgba(255, 0, 0, 0.5);`
3. The final `0.5` strictly sets the opacity to 50%. 
4. Lay a second colored absolutely positioned `<div style="background-color: rgba(0, 0, 255, 0.5)">` partially overlapping the first. Observe physically how the browser's C++ rendering engine mathematically blends the two translucent light signals.

**Part 3: Lossy Compression Artifacts**
1. Find a large, high-definition photograph online.
2. Search for a free online image compressor (e.g., Squoosh.app by Google).
3. Load the image. Aggressively crank the JPEG compression slider mathematically down to 5%.
4. Zoom in completely 500% onto a sharp edge in the photograph natively.
5. You will witness "Mosquito Noise", a distinct physical halo of blocky artifacts. This is the JPEG algorithm failing to rebuild the discarded mathematical matrices around sharp contrast borders accurately.

**Part 4: Imagemagick CLI Manipulation**
1. Install `imagemagick` locally on your computer using your package manager (like `brew install imagemagick` on Mac, or download the Windows binary).
2. Command the CLI engine natively to brutally explicitly convert a high-definition PNG definitively into a garbage-quality 10% JPEG using pure terminal commands:
   `magick convert input.png -quality 10 output.jpg`
3. Compare the file sizes exactly. The size will drop mathematically by roughly 95%, at the explicit cost of massive structural visual damage.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Never use JPEG algorithms to save UI designs, text, or solid flat logos. Lossy algorithms are entirely mathematically designed for smooth photographic gradients organically. Flat solid colors will incur immediate heavy structural artifact damage natively. Always use PNG or SVG for flat graphics.
- **Gotcha 2:** Modern Web Development strictly mandates optimizing images organically. Serving a raw 5MB photograph mathematically completely throttles mobile users' bandwidth dynamically. Implement automated build pipelines using tools natively like Webpack or Vite to permanently automatically convert images to the modern ultra-compressed `WebP` organic format mathematically.

### Reflection Question
If a standard 1080p computer monitor structurally features exactly 1920 by 1080 physical pixels, and each individual pixel mathematically requires 24 bits (3 bytes) of RAM specifically to store the RGB color natively, exactly how many megabytes of raw uncompressed video memory are mathematically required to display a single static image?