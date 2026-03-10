# Exercise 001 - Server Basics (Node & Express)

### Objective
Graduate from building static client browsers. Initialize a persistent virtual server directly on your operating system capable of receiving thousands of concurrent network connections autonomously.

### Core Concepts to Master
- **Node.js Environment:** The V8 JavaScript engine detached entirely from the browser, allowing JS to access raw native system hardware (File System, RAM, Network Interfaces).
- **Express.js Framework:** A lightweight architectural wrapper standardizing incoming raw TCP/HTTP streams into predictable `req` (Request) and `res` (Response) JavaScript objects.
- **Ports:** Virtual docks on your IP address. While standard web traffic explicitly hits Port `80`, development servers traditionally bind locally to unprivileged ports like `3000` or `8080`.

### Research Topics
- "Node JS HTTP module vs Express"
- "Express hello world tutorial"
- "Listening to a port in Node Node"

---

### The Practical Challenge

**Part 1: The Raw Node Server**
1. Initialize a blank `server.js` file natively.
2. Require the built-in HTTP module: `const http = require('http')`.
3. Construct the server natively without frameworks:
   ```javascript
   const server = http.createServer((req, res) => {
       res.statusCode = 200;
       res.setHeader('Content-Type', 'text/plain');
       res.end('Hello World');
   });
   ```
4. Tell the script to actively listen indefinitely: `server.listen(3000)`.
5. Run `node server.js`. Your terminal freezes. The active event loop is now permanently listening.

**Part 2: Express Scaffolding**
1. Standard Node HTTP modules require manually parsing messy byte buffers strictly to extract URLs or JSON bodies safely.
2. Install the industry standard: `npm install express`.
3. Re-write the entire file using Express syntax cleanly:
   ```javascript
   const express = require('express');
   const app = express();
   ```

**Part 3: The GET Endpoint**
1. Construct your primary default route properly:
   ```javascript
   app.get('/', (req, res) => {
       res.send('Hello World via Express');
   });
   ```
2. Finalize the active port sequence: `app.listen(3000, () => console.log('Listening'));`.
3. Boot the server securely.
4. Navigate locally to `http://localhost:3000` inside your physical Chrome browser.

**Part 4: JSON Payloads**
1. REST APIs securely require JSON structures inherently, not plain text.
2. Create a specific secondary distinct route:
   ```javascript
   app.get('/api/users', (req, res) => {
       res.json({ users: ['admin', 'guest'] });
   });
   ```
3. Boot the physical terminal automatically. Navigate to `http://localhost:3000/api/users`.
4. The exact JSON payload smoothly renders.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Assuming file changes reload dynamically. Install `nodemon` to restart servers automatically.
- **Gotcha 2:** Forgetting `JSON.stringify` logic before transmitting native objects over HTTP manually. Express `.json()` handles this automatically.

### Reflection Question
Why do REST API routes structurally mandate explicit HTTP verbs?
