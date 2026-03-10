# Exercise 006 - Applied OCR

### Objective
Leverage Tesseract.js in a full-stack context. Construct an automated scanner pipeline integrating front-end image capturing, Web Workers for background-processing, and RegEx for precise data extraction.

### Core Concepts to Master
- **The Worker Architecture:** Spawning isolated threads in JavaScript to offload intensive OCR model execution without freezing the main UI thread.
- **Data Scraping Pipelines:** Extracting actionable business data (like Prices or Emails) from raw OCR text using regular expressions.
- **Bounding Boxes:** Using spatial coordinate data to identify exactly where text is situated within a raster image.
- **Engine Lifecycle:** Managing the loading, initialization, and termination of OCR workers to optimize memory usage.

### Research Topics
- "JavaScript Web Workers tutorial"
- "Tesseract.js progress logger example"
- "Parsing text OCR using regular expressions"
- "Tesseract.js worker API documentation"

---

### The Practical Challenge

**Part 1: The UI Upload Interface**
1. Construct a React interface containing a file input: `<input type="file" />`.
2. Map the selected file to a local object URL using `URL.createObjectURL(file)`.
3. Display the selected image on the screen using an `<img>` tag.
4. Add a "Scan Document" button to trigger the OCR process.

**Part 2: The Background Worker**
1. To prevent the UI from freezing, initialize Tesseract using its Worker API.
2. Inside your `scan()` function, spawn and configure the worker:
   ```javascript
   import { createWorker } from 'tesseract.js';

   const worker = await createWorker({
       logger: (msg) => console.log(`Progress: ${msg.progress * 100}%`) 
   });
   
   await worker.loadLanguage('eng');
   await worker.initialize('eng');
   ```
3. Use the logger callback to update a progress bar in your UI as the OCR engine processes the image.

**Part 3: Detailed Data Extraction**
1. Execute the recognition process:
   `const { data } = await worker.recognize(imageSource);`
2. Inspect the `data` object in your console. Note that it contains more than just raw text.
3. Explore the nested structure: `data.lines`, `data.words`, and `data.symbols`.
4. Observe the `confidence` scores and `bbox` (bounding box) coordinates for each word to understand how the engine interprets spatial layout.

**Part 4: Implementing RegEx Heuristics**
1. Assume the OCR output is a chaotic block of text (e.g., from a receipt or bill).
2. Your goal is to extract the "Total Amount Due."
3. Write a Regular Expression to search for currency patterns following a label:
   `const regex = /Total(?: Due)?\s*[:$]?\s*(\d{1,4}\.\d{2})/i;`
4. Apply the regex to the `data.text` result and display the extracted amount in your UI.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Memory Leaks. You must call `await worker.terminate()` once the scanning process is complete. If you don't, individual worker threads will stay alive in the background, eventually consuming all available system RAM.
- **Gotcha 2:** Network Latency. Tesseract.js downloads its language models (e.g., `eng.traineddata`) dynamically on the first run. Ensure you have a robust loading state to handle the initialization time.

### Reflection Question
In what scenario would analyzing spatial bounding box coordinates (`data.lines`) be more effective than using a simple Regular Expression to find a price on a complex page layout?