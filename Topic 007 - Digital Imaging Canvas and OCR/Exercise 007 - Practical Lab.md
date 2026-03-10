# Exercise 007 - Practical Lab (Image Processor)

### Objective
Integrate Canvas data manipulation and OCR into a unified, functional processing pipeline. Build an application that accepts visual documents, applies contrast enhancements via Canvas, and extracts the text via WebAssembly Tesseract workers.

### Core Concepts to Master
- **Image Upload Handling:** Parsing `File` objects from native `<input type="file" />` elements and rendering them via `URL.createObjectURL()`.
- **Canvas Image Data Pipeline:** Transferring uploaded images onto a hidden HTML5 `canvas`, applying custom grayscale and contrast filters, and extracting the modified pixel matrix as a raw data blob.
- **Asynchronous Worker Management:** Launching, executing, and terminating a Tesseract.js Web Worker background thread to prevent Main UI lockups.
- **Data Rendering:** Formatting and projecting the returned bounding boxes, text lines, and final parsed strings onto the DOM.

### Research Topics
- "JavaScript File API createObjectURL"
- "HTML5 Canvas drawImage scaling"
- "Tesseract.js progress bar React"
- "Applying threshold filter HTML5 canvas"

---

### The Practical Challenge

**Part 1: The Upload and Image Render Shell**
1. Initialize a Vite React project.
2. Construct a basic UI with a file input, a large image display container, and a "Process Document" button.
3. Capture the uploaded file and set it in a React state `const [imageSrc, setImageSrc] = useState(null)`.
4. Render an `<img>` tag that displays the `imageSrc`. Connect the UI so the user sees the document they just uploaded.

**Part 2: The Hidden Contrast Canvas**
1. Create an off-screen `<canvas>` reference (using `useRef` in React).
2. When the user clicks "Process Document", draw the current `<img>` into the canvas using `ctx.drawImage()`.
3. Extract the `ImageData` array.
4. Implement a loop over the pixel array: calculate the RGB average for each pixel. If the average is below a set threshold (e.g., 100), force it to absolute black (`0, 0, 0`); otherwise, force it to absolute white (`255, 255, 255`).
5. Write the modified pixel matrix back to the canvas. The document should now look like a high-contrast black-and-white photocopy.
6. Convert the canvas back into a Base64 string using `canvas.toDataURL()`.

**Part 3: The OCR Web Worker Pipeline**
1. Pass the new, high-contrast Base64 string into Tesseract.js.
2. Initialize a worker instance using `createWorker`.
3. Add a `logger` callback to the worker configuration. Catch the `progress` float values and map them to a physical HTML progress bar element (`<progress value="50" max="100">`).
4. Ensure the UI visually feedback is responsive while the engine trains the language and processes the image.

**Part 4: Data Parsing and Cleanup**
1. Once `recognize()` resolves, extract `result.data.text`.
2. Assume the document is an invoice. Write a simple regex to find the word *Total* followed by a price, such as `/Total[\s:]*\$?(\d+\.\d{2})/i`.
3. Render both the full raw text block and the extracted regex price value securely onto the screen.
4. Conclude the operation by invoking `await worker.terminate()` to clean up processor memory.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Trying to draw an image onto a Canvas before the image is fully loaded. Drawing an `<img>` tag that is still fetching its `src` will result in a blank canvas. Ensure you utilize the `.onload` event handler before triggering `ctx.drawImage()`.
- **Gotcha 2:** CORS (Cross-Origin Resource Sharing) blocked errors when using Tesseract on external image URLs. Only pass local file blobs or Base64 data URLs to Tesseract to avoid security network blocks.

### Reflection Question
What is the structural impact on memory and battery life if a user repeatedly clicks the scan button, and your code initializes a new 30MB Tesseract worker array every single time without ever invoking `.terminate()`?
