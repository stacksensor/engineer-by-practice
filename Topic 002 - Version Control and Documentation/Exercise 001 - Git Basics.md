# Exercise 001 - Git Basics

### Objective
Initialize version control for a project. Understand the core workflow of tracking changes iteratively, recognizing file states, and creating snapshots (commits) in Git.

### Core Concepts to Master
- **Version Control System (VCS):** Explaining Git as a time machine that records exact line-by-line changes across sets of files.
- **The Three States of Git:**
  - *Working Directory (modified):* You have changed a file on disk but not committed it to the database.
  - *Staging Area (staged/index):* You have marked a modified file to be included in your next commit snapshot.
  - *.git directory (committed):* The data is safely and permanently stored in your local repository database.
- **Commits:** Permanent, immutable snapshots of your project graph paired with an explanatory message.

### Research Topics
- "What is Git vs GitHub?"
- "Git lifecycle stages (add, commit, status)"
- "Git working directory vs staging area"
- "How to write a professional git commit message"

---

### The Practical Challenge

**Part 1: Initialization and the Working Directory**
1. Open your terminal and create a new directory: `mkdir git_practice && cd git_practice`.
2. Initialize version control: `git init`. (Notice the "Initialized empty Git repository" message).
3. Check the condition of the project: `git status`. It should say you are on branch `main` (or `master`) and there is nothing to commit.
4. Create an `index.html` file using your CLI skills: `touch index.html`.
5. Run `git status` again. Notice `index.html` is now red and listed under "Untracked files".

**Part 2: The Staging Area**
1. Add the file to Git's awareness (Staging Area): `git add index.html`.
2. Run `git status` again. The file is now green and listed under "Changes to be committed".
3. Modify the file without commiting. Use `echo "<h1>Hello World</h1>" > index.html`.
4. Run `git status`. You will see `index.html` listed **twice**: once in green (the empty version you staged) and once in red (the new changes you just made).
5. Stage the new changes: `git add index.html`. The red version disappears.

**Part 3: Commits and History**
1. Permanently snapshot the staging area into a Commit: `git commit -m "Initialize project with core HTML file"`.
2. Run `git status` to verify the working tree is clean.
3. View your project history log: `git log`. Note the massive hash string (e.g., `a1b2c3d`), your author name, the date, and the message.
4. Make a second modification: `echo "<p>This is paragraph two</p>" >> index.html`.
5. Run `git diff`. This highlights exact line additions (in green `+`) and deletions (in red `-`) before you stage them.
6. Stage the changes (`git add .`) and commit them with a message: `git commit -m "Add a second paragraph to index"`.

**Part 4: Ignoring Files**
1. Create a secret configuration file containing fake passwords: `touch secrets.env`.
2. Run `git status`. It immediately prompts you to track `secrets.env`. **Do not do this.**
3. Create a `.gitignore` file: `touch .gitignore`.
4. Add the name of your secrets file to the ignore list: `echo "secrets.env" > .gitignore`.
5. Run `git status`. Notice that `secrets.env` has vanished from Git's radar, but `.gitignore` is now an untracked file ready to be committed!

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Forgetting to run `git add` before `git commit`. Git does not care what files you have modified on your hard drive; it only commits exactly what is sitting in the Staging Area.
- **Gotcha 2:** Writing poor, unhelpful commit messages like `"wip"`, `"fixed stuff"`, or `"updated code"`. If your commit message cannot finish the sentence *"If applied, this commit will..."*, rewrite it.
- **Gotcha 3:** Never, ever track hardcoded passwords or API keys (like AWS or Stripe keys). If they get pushed to GitHub accidentally, bots will steal them instantly. Use `.gitignore` religiously.

### Reflection Question
If you modify `style.css`, add it to the staging area with `git add`, then immediately change `style.css` again on disk, what happens when you type `git commit` without running `git add` a second time?
> *Hint: Understand the hard separation between the Working Directory and the Staging Area.*