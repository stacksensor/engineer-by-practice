# Exercise 002 - Git Internals

### Objective
Demystify what Git actually does under the hood and learn branching basics for isolated feature development. Understand that Git is essentially a simple key-value data store built upon cryptic hashes.

### Core Concepts to Master
- **The `.git` directory:** The hidden folder where Git stores all your project history, objects, and configurations. Never manually delete this folder—or any files inside—unless you want to permanently erase your version history!
- **Hashes (SHA-1 algorithms):** The unique 40-character hexadecimal string identifying every single commit, tree, and blob (file content).
- **Branches:** Extremely lightweight pointers to specific commits. They allow you to diverge from the main line of development, work independently on a new feature, and merge your changes back seamlessly.

### Research Topics
- "Git internals architecture (.git folder)"
- "What does the HEAD pointer do in Git?"
- "Git branching and merging for beginners"
- "How to resolve Git merge conflicts manually"

---

### The Practical Challenge

**Part 1: Peeking Under the Hood**
1. Continue using yesterday's `git_practice` repository via your terminal.
2. Run `ls -a` (List All). Notice the hidden `.git` folder you initialized yesterday.
3. Dive into the underlying database: type `cat .git/HEAD`. 
   You will see text matching `ref: refs/heads/main` (or `master`). This file tells Git *exactly* which branch your currently active workspace is pointing to.
4. Run `git log` and copy the top (most recent) hash string (e.g., `a45c91b...`).
5. Run `git show <that_hash_string>`. The terminal will spit out the exact diff of what changed during that specific point in time!

**Part 2: Branching Out**
1. Let's create an isolated workspace for a new feature. Create a branch named `feature-login`: 
   `git branch feature-login`.
2. Nothing seemingly happens. Switch your active directory over to that new pointer: 
   `git checkout feature-login` (or on newer Git versions: `git switch feature-login`).
3. Run `git status` to verify you are on `feature-login`.
4. Create a placeholder script: `touch login.js`.
5. Stage and commit it: `git add login.js` then `git commit -m "Add initial login placeholder"`.
6. Run `ls` to see the `login.js` file sitting next to `index.html`.

**Part 3: Time Travel and File Swapping**
1. Switch back to your old, safe codebase: `git checkout main` (or `master`).
2. Run `ls`. **Notice that `login.js` has vanished from your hard drive!** 
   Git instantaneously replaced your entire folder's contents with the snapshot mapped locally to the `main` branch pointer.
3. Switch forward again: `git checkout feature-login`. Run `ls`. The `login.js` file reappears.
4. Switch back to `main` one final time. We are now ready to unify the history.

**Part 4: Merging Branches**
1. Ensure your active branch is `main` (`git status`).
2. Pull the changes from your feature branch into the current one: `git merge feature-login`.
3. If no other commits were made on `main` while you were away, Git will execute a "Fast-forward" merge.
4. Run `ls`. `login.js` is now permanently incorporated into `main`!
5. Clean up your pointer list since the feature is complete: `git branch -d feature-login`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Switching branches while you have uncommitted changes in your Working Directory can cause massive headaches. Git may try to carry them over, or it may entirely block the switch with a "Please commit or stash your changes" error. Always run `git status` and commit before switching.
- **Gotcha 2:** Visualizing branches as complete parallel "copies" of folders is incorrect. A branch in Git is literally a tiny text file holding a 40-character string pointing to a commit object in your database.
- **Gotcha 3:** Merging *always* brings changes **into** your active branch. Therefore, if you want `feature-A` changes added to `main`, you must be sitting on `main` when executing the merge command.

### Reflection Question
How does Git physically know what specific files belong in your folder when you type `git checkout main`?
> *Hint: Think back to Part 1 and what file stores your current location.*