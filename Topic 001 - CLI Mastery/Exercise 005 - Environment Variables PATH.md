# Exercise 005 - Environment Variables & PATH

### Objective
Configure your environment for professional development. Understand how the shell locates executables using the `PATH` variable and how to manage environment-specific configurations (API keys, themes, aliases) using profile configuration files (.zshrc / .bash_profile).

### Core Concepts to Master
- **Environment Variables:** Global key-value pairs (`HOME`, `USER`, `PATH`) that influence the behavior of the shell and child processes.
- **The PATH Variable:** A colon-separated list of directories where the shell searches for commands.
- **Shell Profiles:** Initialization scripts (`.zshrc`, `.bashrc`) that run every time a new terminal session starts.
- **Aliases:** Creating short "nickname" commands for long, complex terminal strings.

### Research Topics
- "How to add a directory to PATH on Mac/Linux"
- "Difference between .bashrc and .bash_profile"
- "What do export and env commands do"
- "Creating persistent aliases in Zsh"

---

### The Practical Challenge

**Part 1: Investigating the PATH**
1. Print your current path: `echo $PATH`.
2. Identify at least three different directories in the list.
3. Use the `which` command to find where the `ls` and `python` (or `node`) executables are physically located. 
4. Check if those locations are inside one of your PATH directories.

**Part 2: Temporal PATH Modification**
1. Create a directory named `mytools` in your home folder.
2. Create a simple script inside called `hello` that prints "Hello World". Make it executable.
3. Try to run `hello` from a different directory. It will fail.
4. Manually add `~/mytools` to your current session's path: `export PATH="$PATH:$HOME/mytools"`.
5. Run `hello` again. It now works from anywhere!

**Part 3: Persistent Configuration**
1. Open your shell configuration file (e.g., `~/.zshrc` or `~/.bash_profile`).
2. Add your `export PATH` line to the bottom of the file.
3. Add a custom alias: `alias gs="git status"`.
4. Save and restart your terminal (or run `source ~/.zshrc`).
5. Verify that `hello` and `gs` work in the brand new session.

**Part 4: Managing Secrets**
1. Practice setting temporary variables: `export API_KEY="secret123"`.
2. Use `printenv` or `env` to see all active environment variables.
3. Write a tiny script that "reads" the `API_KEY` variable and prints "Connecting with key...".
4. Discuss why you should *never* commit sensitive `export` lines to a public GitHub repository.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** PATH Order. The shell searches directories from left to right. If you have two versions of `node` installed, the one in the directory that appears *first* in your PATH is the one that will run.
- **Gotcha 2:** Syntax Errors in Profiles. If you make a mistake in your `.zshrc`, your terminal might stop working or crash on startup. Keep a backup or use a secondary editor to fix the file if the terminal breaks.

### Reflection Question
Why is the `PATH` variable considered the most critical environment variable for a software developer's machine setup?
