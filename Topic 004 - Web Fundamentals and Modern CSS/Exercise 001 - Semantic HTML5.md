# Exercise 001 - Semantic HTML5

### Objective
Structure a webpage using proper Semantic HTML tags to dramatically improve Search Engine Optimization (SEO), document outline, and raw readability before applying any CSS.

### Core Concepts to Master
- **"Div Soup":** The amateur practice of using `<div>` for every single block of content on a page. A computer cannot derive meaning from a `<div>`.
- **Semantic Tags:** HTML5 introduced tags that inherently describe the *meaning* of the content they wrap. (`<header>`, `<nav>`, `<main>`, `<footer>`, `<article>`, `<aside>`, `<section>`).
- **Heading Hierarchy:** Properly nesting `<h1>` down to `<h6>` tags. Multiple `<h1>` tags per page usually harm SEO.

### Research Topics
- "HTML5 Semantic Elements guide"
- "Why use semantic HTML over divs"
- "HTML Document Object Model (DOM) Tree"

---

### The Practical Challenge

**Part 1: The Boilerplate**
1. Create a folder `web_basics`. Inside it, create `index.html`.
2. Open the file in VS Code. Type `!` and press Tab to auto-generate the HTML5 boilerplate.
3. Observe the `<html>`, `<head>`, and `<body>` tags. 
4. In the `<head>`, update the `<title>` to "Tech Blog". 
5. Add a `meta` description tag for SEO: `<meta name="description" content="A blog about learning modern web development.">`

**Part 2: The Document Outline**
1. Inside the `<body>`, structure the core skeleton using semantic tags (do not add actual text yet).
2. Create:
   - A `<header>` at the top.
   - A `<main>` block underneath it.
   - A `<footer>` at the bottom.
3. Inside the `<header>`, add a navigation bar using the `<nav>` tag, containing an unordered list `<ul>` with three list items `<li>` linking to Home, About, and Contact using `<a>` tags.
4. Inside the `<main>`, add an `<aside>` block to act as a sidebar, and a `<section>` block to hold the primary blog articles.

**Part 3: Content Population**
1. Inside your `<footer>`, add a copyright symbol using the HTML entity `&copy; 2026 Your Name`.
2. Inside the `<section>` for your articles, create two `<article>` tags.
3. Inside each `<article>`, provide a strict heading hierarchy: An `<h2>` for the title, an `<h3>` for the date/author, and two `<p>` tags for the paragraphs of dummy text (use `lorem20` in VS Code to generate placeholder text).
4. Do not use a *single* `<div>` tag anywhere in this entire document.

**Part 4: Validating Output**
1. Open your `index.html` file in the Chrome browser (drag and drop the file, or use an extension like 'Live Server').
2. Observe how visually boring it is. Semantic HTML applies almost zero styling—it focuses purely on structure.
3. Right-click the page and hit "Inspect" to open Chrome Developer Tools. Click the "Elements" tab.
4. Expand your `<body>` tag and hover over your `<main>` and `<article>` tags to see how Chrome highlights the rectangular layout boxes.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Do not use `<section>` purely as a stylistic wrapper (like you would a `<div>`). A `<section>` should theoretically always contain a heading (`<h2>`-`<h6>`) summarizing its distinct thematic group of content.
- **Gotcha 2:** Only use one `<main>` tag per page. It represents the dominant content for that URL, hiding things like standard sidebars and navigation headers.
- **Gotcha 3:** A `<header>` does not replace the `<head>` of a document. The `<head>` contains invisible metadata for the browser/server. The `<header>` contains visible content (like logos and menus) for the user.

### Reflection Question
If you are completely blind and relying on software called a "Screen Reader" to read a webpage out loud to you, why does hitting the 'Tab' key to jump directly between `<article>` tags provide a drastically better user experience than if the developer had just built the entire page out of `<div>` tags?