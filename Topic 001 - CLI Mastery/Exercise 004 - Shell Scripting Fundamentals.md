# Exercise 004 - Shell Scripting Fundamentals

### Objective
Automate redundant tasks. Move beyond running single commands to writing robust, reusable shell scripts (Bash/Zsh) that use variables, loops, and conditional logic to orchestrate complex file and system operations.

### Core Concepts to Master
- **The Shebang (`#!`):** Instructing the kernel which interpreter to use for the script.
- **Variables & Arguments:** Capturing user input and storing temporary data within a script.
- **Conditional Logic (`if/then/else`):** Making decisions based on file existence, command success, or string matching.
- **Loops (`for/while`):** Performing repetitive actions across multiple files or directories automatically.

### Research Topics
- "Bash scripting for beginners"
- "How to use variables in shell scripts"
- "Bash if-else and comparison operators"
- "Looping through files in a directory bash"

---

### The Practical Challenge

**Part 1: The First Script**
1. Create a file named `backup.sh`.
2. Add the shebang as the first line: `#!/bin/bash`.
3. Add a command to create a directory named `backups`.
4. Make the script executable: `chmod +x backup.sh`.
5. Run it: `./backup.sh`.

**Part 2: Variables and Arguments**
1. Modify your script to accept a filename as an argument: `./backup.sh myfile.txt`.
2. Use `$1` to access the first argument.
3. Add logic to copy the specified file into the `backups` directory, appending a timestamp to the filename: `cp $1 backups/$1_$(date +%Y%m%d)`.

**Part 3: Conditionals and Safety**
1. Add an `if` statement to check if the file provided actually exists using the `-f` flag.
2. If it doesn't exist, print an error message and exit with a non-zero status code: `exit 1`.
3. Add a check to see if the `backups` folder already exists before trying to create it using the `-d` flag.

**Part 4: Batch Processing with Loops**
1. Extend the script to handle multiple files.
2. If the user provides a directory path, use a `for` loop to backup every `.txt` file inside that directory.
3. Add a "Logging" feature: Every time a file is backed up, append the filename and timestamp to a `backup_log.txt` file.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Spaces in Variables. If a filename has a space, `$1` will break. Always wrap your variables in double quotes: `"$1"`.
- **Gotcha 2:** Windows Line Endings. If you edit a script in a Windows editor and run it on Linux/Mac, the invisible `\r` characters will cause cryptic "command not found" errors. Use `dos2unix` to fix.

### Reflection Question
Why is shell scripting often preferred over Python or Node.js for simple system-level tasks like moving files or managing logs?
