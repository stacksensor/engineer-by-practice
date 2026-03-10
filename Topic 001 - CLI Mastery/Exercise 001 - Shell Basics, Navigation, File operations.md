# Exercise 001 - Shell Basics, Navigation, File operations

### Objective
Master navigating the filesystem and performing basic file operations entirely from the terminal without using the mouse. You will learn how to orient yourself in the system, create directories, manipulate files, and clean up.

### Core Concepts to Master
- **The Shell / Terminal:** The graphical window you type into is the "Terminal Emulator". The program running inside it that understands your commands is the "Shell". Common shells include Bash (Bourne Again Shell) and Zsh (Z Shell, default on modern macOS). 
- **Current Working Directory (CWD):** The folder your shell is currently operating in. Every relative command you type executes from this location.
- **Paths:** 
  - **Absolute Paths:** The full address of a file starting straight from the root directory of the hard drive (`/`). Example: `/Users/john/Documents/report.txt`
  - **Relative Paths:** The address of a file relative to where you currently are. `.` refers to the current directory. `..` refers to the parent directory. Example: `../Downloads/image.png`

### Research Topics
- "Zsh vs Bash differences beginner"
- "Linux file system navigation (pwd, cd, ls)"
- "Linux file manipulation (touch, mkdir, cp, mv, rm)"
- "What does the tilde `~` mean in Linux?"

---

### The Practical Challenge

**Part 1: Orientation and Navigation**
1. Open your terminal application (e.g., iTerm2, macOS Terminal, or VS Code integrated terminal).
2. Type `pwd` (Print Working Directory) and hit Enter. Note the exact path output.
3. Type `cd ~` (Change Directory to Home). Run `pwd` again. You should be in your user's home folder.
4. Type `ls` (List) to see all visible files and folders. 
5. Type `ls -la` to see *all* files (including hidden ones that start with a `.`) formatted as a detailed list. Notice the permission strings on the left (e.g., `drwxr-xr-x`).

**Part 2: Creation and Manipulation**
1. Ensure you are in your home directory (`cd ~`).
2. Create a new folder: `mkdir terminal_practice`.
3. Move into that folder: `cd terminal_practice`.
4. Create a deeply nested structure with one command: `mkdir -p project_alpha/src/components`.
5. Navigate into `project_alpha`: `cd project_alpha`.
6. Create three empty files: `touch index.html style.css app.js`.
7. Verify they exist: `ls`.

**Part 3: Moving and Renaming**
1. Create a `css` folder and a `js` folder: `mkdir css js`.
2. Move your stylesheet: `mv style.css css/`.
3. *Rename* and move your JavaScript file combining both actions into one command: `mv app.js js/main.js`. 
  *(Note: In Linux, `mv` is used for both moving and renaming).*
4. Run `ls -R` (Recursive list) to view the entire tree structure of `project_alpha` to ensure the files ended up in the right folders.

**Part 4: Destruction**
1. Navigate back to `terminal_practice`: `cd ..`.
2. Attempt to delete `project_alpha` using `rm project_alpha`. Observe the error message saying it is a directory.
3. Forcefully and recursively delete the directory and everything inside it: `rm -rf project_alpha`.
4. Delete the parent directory to clean up your home folder: `cd ..` then `rmdir terminal_practice` (since it's now empty).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Using `rm` without `-r` on a directory will fail. Directories must be removed recursively (`rm -r`). Adding `-f` bypasses confirmation prompts—use with extreme caution!
- **Gotcha 2:** Spaces in file names cause bash to interpret them as separate arguments. If you type `mkdir Hello World`, it creates two folders. To create one, use quotes: `mkdir "Hello World"` or escape the space: `mkdir Hello\ World`.
- **Gotcha 3:** The command `cd` (with no arguments) will instantly teleport you back to your home directory (`~`). `cd -` will teleport you to your previously visited directory.

### Reflection Question
If you are currently inside `/Users/john/Documents/work` and you want to copy a file `/Users/john/Downloads/cat.jpg` into your current directory, what is the shortest command you can type using relative paths and shorthand?
> *Hint: Think about what `.` means.*