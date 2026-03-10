# Exercise 002 - Shell Mastery: Ripgrep & CLI Power Tools

### Objective
Command the machine. Master **Shell Productivity**—the art of using the Command Line (CLI) to find, change, and manage text at the speed of light. Learn how to use **ripgrep (rg)**, **sed**, and **fzf** to find a single line of code in a 1,000,000-line project in seconds.

### Core Concepts to Master
- **ripgrep (rg):** The high-speed search tool that replaces `grep`. (The "Gold Standard" for developers).
- **fzf (Fuzzy Finder):** Searching for files or commands by typing "Part" of the name. (e.g., `fzf` -> `pro` -> `profile.js`).
- **sed:** A "Stream Editor" for find-and-replace using the command line. (e.g., `sed 's/old/new/g' file.txt`).
- **Pipes (|):** Passing the output of one command to the input of another. (The "Unix Philosophy").
- **Aliases:** Custom "Shortcuts" for long commands. (e.g., `alias gs='git status'`).

### Research Topics
- "How to use ripgrep (rg) for searching code"
- "Introduction to fzf: The fuzzy finder for the command line"
- "Basic 'sed' find-and-replace command examples"
- "Building a 'Toolbox' of shell aliases in your .zshrc"

---

### The Practical Challenge

**Part 1: The "Manual" Search (Scenario)**
1. You have 1,000 files. You want to find every line that says `TODO: Fix this`.
2. Using a standard "Finder" or "Explorer" search (Wait 30 seconds).
3. Using **ripgrep**: `rg "TODO: Fix this"`. (Time: 0.1s).
4. Discuss: Why does a "Fast" search make you more likely to actually "Fix" the code?

**Part 2: The "Fuzzy" Finder (fzf)**
1. Research how to "Pipe" a list of files into **fzf**: `find . | fzf`.
2. Discuss how this is better than scrolling through 100 folders in VS Code.
3. Extra: Research the **`CTRL-R`** shortcut for fzf. (Finding a command you typed 3 days ago).

**Part 3: The "Batch" Replace (sed)**
1. You have a file `config.txt` and you want to change "localhost" to "127.0.0.1" on every line.
2. In the terminal: `sed -i 's/localhost/127.0.0.1/g' config.txt`. 
3. Discuss: If you have **50 files** to change, how does a `for` loop + `sed` save you 1 hour of manual work? (Answer: It does it in 1 second!).

**Part 4: Identifying the "Tool"**
1. Which tool for:
   - "Searching for text INSIDE files" (Answer: `rg`).
   - "Searching for FILE NAMES" (Answer: `fzf` or `find`).
   - "Counting the number of lines in a file" (Answer: `wc -l`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Accidentally overwriting a file with `sed -i`. If you make a mistake in your "Regex," you might delete all the text in your file. Always use `sed` *without* the `-i` flag first to see if the output is what you expect!
- **Gotcha 2:** Complicated regular expressions. Don't spend 1 hour writing a complex `sed` command if you could have done it in 5 minutes by hand. Only "Automate" when the task is repetitive enough to matter.

### Reflection Question
Why is the "Command Line" considered the most powerful tool for a software engineer, despite its steep learning curve? (Answer: Because it allows you to "Script" your actions and combine tools in ways a Mouse and GUI never can).
