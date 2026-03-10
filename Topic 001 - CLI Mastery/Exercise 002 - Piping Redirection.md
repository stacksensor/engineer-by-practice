# Exercise 002 - Piping & Redirection

### Objective
Understand how to connect the output of one command to the input of another, and how to save terminal output directly into text files. You will learn to manipulate data streams efficiently.

### Core Concepts to Master
- **Standard Streams:** When a command runs in Linux, it uses three standard streams for handling data: 
  - `stdin` (0): Standard Input (what you type or pipe in).
  - `stdout` (1): Standard Output (the normal results printed to the screen).
  - `stderr` (2): Standard Error (error messages printed to the screen).
- **Piping (`|`):** A method to take the `stdout` of the command on the left and feed it directly as the `stdin` to the command on the right.
- **Redirection (`>`, `>>`):** Grabbing the output of a command and sending it to a file instead of the screen. `>` overwrites the file, `>>` appends to it.

### Research Topics
- "Linux standard input, standard output, standard error explained"
- "How to use the pipe symbol in bash"
- "Output redirection in bash (> vs >>)"
- "What is /dev/null in Linux?"

---

### The Practical Challenge

**Part 1: Text Creation and Redirection**
1. Open your terminal and create a new folder: `mkdir streams_practice && cd streams_practice`.
2. Use the `echo` command to print a string: `echo "System initialized"`.
3. Redirect that output into a file: `echo "System initialized" > system.log`.
4. Read the file to ensure it worked: `cat system.log`.
5. Now, use `echo "User logged in"` but use `>>` to append it: `echo "User logged in" >> system.log`.
6. Read the file again. Notice that `>` destroys the old file, while `>>` preserves it.
7. Try `echo "Warning: Low disk space" > system.log`. Note how it erased your previous two lines.

**Part 2: Piping Commands Together**
1. Let's create a larger file. Run: `ls -la /etc > etc_contents.txt`. This dumps the contents of the huge `/etc` folder into a text file.
2. The file is too long to easily read. Use `cat` and pipe it into `less`: `cat etc_contents.txt | less`. (Press `q` to exit `less`).
3. Pipe the output to `wc -l` (word count - lines) to see exactly how many lines are in the file: `cat etc_contents.txt | wc -l`.
4. Let's pipe three commands! Read the file, filter for the word "network" using `grep`, and count the results: 
   `cat etc_contents.txt | grep -i "network" | wc -l`.

**Part 3: Managing Errors (stderr)**
1. Try to list a directory that doesn't exist: `ls /nonexistent_folder`. You will see an error on the screen.
2. Try redirecting that output to a file: `ls /nonexistent_folder > normal_output.txt`. 
   Notice the error still prints to the screen! The file `normal_output.txt` will be totally empty.
3. This is because `>` only redirects `stdout` (1). Errors use `stderr` (2). 
4. Redirect the error specifically by using `2>`: `ls /nonexistent_folder 2> error.log`. Read `error.log` to see the message.
5. Create a scenario with both success and errors: `ls /etc /nonexistent_folder`. 
6. Redirect successes to a file, and errors to a "black hole": 
   `ls /etc /nonexistent_folder > success.txt 2> /dev/null`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** A single misspelled `>` instead of `>>` while trying to add a new line to an important config file will instantly wipe the entire file forever. 
- **Gotcha 2:** Standard piping (`|`) only pipes `stdout` by default, not `stderr`. If a command fails on the left side of the pipe, the error text won't be sent to the right side; it will just print to your screen.
- **Gotcha 3:** `less` acts like a "pager" allowing you to scroll. You cannot type new commands while inside `less`. You must press the `q` key to quit back to your prompt.

### Reflection Question
If you have a Python script `backup.py` run by a server every night, why would running `python3 backup.py > cron.log 2>&1` be a crucial practice? 
> *Hint: Look up what `2>&1` means in relation to stdout and stderr.*