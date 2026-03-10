# Exercise 007 - Parsing Logs with Regex

### Objective
Parse structurally repetitive but noisy data files (like application server logs) using Regex to extract structured insights and business metrics.

### Core Concepts to Master
- **Log formats:** Standardizing the understanding of text logs (e.g., Apache/NGINX logs, Application error traces).
- **Data Cleanup Pipelines:** Moving raw unstructured text -> Regex Extract -> JSON Arrays -> Analytics/Database.
- **Combined Scripts:** Tying native File I/O algorithms to Regex loops to process massive files without crashing your RAM.

### Research Topics
- "Format of NGINX access log"
- "Node JS read file line by line readline module"
- "Regex grouping to extract log columns"

---

### The Practical Challenge

**Part 1: Generating Test Data**
1. Create a `parser` folder. Inside, create a file `access.log` and paste these 5 dummy NGINX lines:
   ```text
   192.168.1.1 - - [25/Oct/2023:10:00:01 +0000] "GET /index.html HTTP/1.1" 200 1024
   10.0.0.55 - - [25/Oct/2023:10:05:12 +0000] "POST /api/login HTTP/1.1" 401 512
   192.168.1.1 - - [25/Oct/2023:10:11:45 +0000] "GET /images/logo.png HTTP/1.1" 200 4096
   172.16.0.2 - - [25/Oct/2023:10:15:22 +0000] "DELETE /api/user HTTP/1.1" 403 128
   10.0.0.55 - - [25/Oct/2023:10:20:01 +0000] "GET /dashboard HTTP/1.1" 500 0
   ```
   
**Part 2: Devising the Pattern**
1. Open Regex101 and load a line of the log.
2. Build a capture group schema chronologically across the line.
   - Group 1 (IP): `^(\S+)`
   - Ignore the dashes.
   - Group 2 (Timestamp): `\[(.*?)\]`
   - Group 3 (Method): `"(GET|POST|PUT|DELETE)`
   - Group 4 (Path): `(\S+) HTTP`
   - Group 5 (Status Code): `.*?" (\d{3})` 
3. Tweak the pattern until the right panel flawlessly extracts all 5 logical groups into memory for every single line.

**Part 3: The Parsing Pipeline Script**
1. Create `parse.js` (or `parse.py`). 
2. Write the code to read the `access.log` file natively into memory, splitting it by `\n` (newlines) into an array of strings.
3. Loop through every line. Run your regex `.match()` or `.search()` against the line.
4. Instead of leaving it as messy tuples, construct a structured JavaScript Object (or Python Dictionary):
   `{ ip: match[1], timestamp: match[2], method: match[3], path: match[4], status: match[5] }`
5. Push this object into a master `results` array. Console.log the final structured array.

**Part 4: Data Analytics via Code**
1. Underneath your parsing loop, write a native JavaScript/Python filter/reduce to answer business questions:
   - Filter the objects to find all logs where `status >= 400` (Errors/Failures). Print them to the console.
   - Write a `reduce` or manual loop to tally exactly how many times each unique IP address hit the server (Hint: build a frequency hashmap).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Server log files can reach Gigabytes in size. If you use standard `fs.readFileSync` or `.read()` to load a 5GB text file instantly into a variable, your script will crash out of RAM. In real scripts, use the `readline` system module to stream the file 1 line at a time.
- **Gotcha 2:** Log patterns often have weird anomalies (e.g., a missing 'HTTP' tag on a malformed hacking request). If your regex relies entirely on absolute strictness, it will randomly skip massive amounts of lines. Build fallback optionality `?` into your patterns.
- **Gotcha 3:** Regex extraction casts everything to a String by default. If you compare `status >= 400`, ensure you coerce `match[5]` into a Number first, or JavaScript will compare string lexicons (`'400' > '50'` triggers weird behavior).

### Reflection Question
If you have a 10 gigabyte NGINX access log on a Linux production server and your boss urgently asks "How many 404 errors happened today?", why shouldn't you write a node.js parsing script like this, and what ultra-fast, native Linux CLI tool (from Topic 1) should you pipeline together instead?