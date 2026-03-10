# Exercise 003 - Advanced CLI Tools

### Objective
Learn to quickly search, find, and manipulate text and files across complex directory structures using advanced CLI utilities. You will wield the true power of the terminal over graphical file explorers.

### Core Concepts to Master
- **`find`:** A command to search the entire filesystem heirarchy for files based on their name, size, type, or access time.
- **`grep` (Global Regular Expression Print):** A command-line utility for searching plain-text data sets line-by-line for matches against a pattern.
- **`awk` / `sed` basics:** 
  - `sed` (Stream Editor) modifies text as it's being read line by line.
  - `awk` is a powerful report-generation language that processes text in columns and rows.

### Research Topics
- "Linux find command examples directory search"
- "Grep tutorial searching files recursively"
- "Recursive vs flat searching in Linux"
- "Sed stream editor basic string replacement"

---

### The Practical Challenge

**Part 1: Generating Test Data**
1. Open your terminal and create a sandbox directory: `mkdir search_sandbox && cd search_sandbox`.
2. Inside it, create ten randomized text files spread across a nested folder structure:
   - `mkdir level1 level1/level2 level1/level2/level3`
   - Create empty text files with random names in each folder using `touch`. 
   - Example: `touch file_a.txt level1/file_b.md level1/level2/file_c.txt level1/level2/level3/data.xml`
3. Into three of those files, use `echo` and `>` to write the word "password": `echo "admin_password: 12345" > level1/level2/file_c.txt`

**Part 2: The `find` Command**
1. In your `search_sandbox` root, use `find` to list every single file and folder ending in `.txt`:
   `find . -name "*.txt"` (The `.` means start checking from the current directory downwards).
2. Modify the search to ignore case using `-iname`: `find . -iname "*.TXT"`.
3. Locate all files larger than 1 megabyte across your entire system (this might take a few minutes): `find / -type f -size +1M 2>/dev/null`.
   *(You pipe errors to `/dev/null` because `find` will hit Permission Denied errors on system files).*

**Part 3: The `grep` Command**
1. Use `grep` to search standard input: `echo "Hello password world" | grep "password"`.
2. Use `grep` to search recursively (`-r` or `-R`) through all your nested folders to find exactly which files contain the text "password":
   `grep -r "password" .`
3. Notice how it prints the filename, a colon, and the matching line of text.
4. Try adding `-n` flag to view the line number, and `-i` to ignore case: `grep -rni "PASSWORD" .`
5. Print ONLY the filenames holding the match using `-l` (lowercase L): `grep -rl "password" .`

**Part 4: The Stream Editor `sed`**
1. Open a new file `database.txt` and fill it with 5 lines containing the word "apple":
   ```bash
   echo "I like apple pie." > database.txt
   echo "The apple is red." >> database.txt
   echo "No apple today." >> database.txt
   ```
2. Use `sed` to replace every occurrence of "apple" with "orange" and output the result to the screen: 
   `sed 's/apple/orange/' database.txt`. 
   *(Notice that the original file `database.txt` remains unchanged).*
3. To edit the file **in-place** (permanently changing it), add the `-i` flag (Warning: on macOS use `-i ''`):
   macOS: `sed -i '' 's/apple/orange/g' database.txt`
   Linux: `sed -i 's/apple/orange/g' database.txt`

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** `grep` is case-sensitive by default. Remember the `-i` flag for case-insensitive searches.
- **Gotcha 2:** `sed` syntax (`s/old/new/g`) can be extremely picky. The `s` stands for substitute, and the `g` stands for global (meaning all instances on that line, not just the first one).
- **Gotcha 3:** When using `find`, you must wrap your search pattern in quotes (e.g., `"*.txt"`). Otherwise, Bash attempts to expand the `*` before passing it to the `find` command, causing strange errors.

### Reflection Question
Why is it often exponentially faster to use an absolute terminal search like `grep -rl` across thousands of files rather than using a graphical text editor's "Search all files" feature?
> *Hint: Consider how graphical software loads files into RAM vs how CLI utilities interact directly with the C-level filesystem APIs.*