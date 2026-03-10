# Exercise 003 - Advanced Git

### Objective
Master advanced Git operations for navigating through history, resolving conflicting changes, temporarily shelving work, and rewriting commit history safely.

### Core Concepts to Master
- **Git Rebase:** Rewriting history by moving or combining a sequence of commits to a new base commit (creating a linear history rather than a messy web of merge nodes).
- **Cherry-pick:** Extracting and applying the specific changes introduced by a single existing commit into a totally different branch.
- **Git Stash:** Temporarily shelving (saving) modified, tracked files without committing them to the permanent database. Useful when you need to urgently switch branches but aren't ready to commit half-finished work.

### Research Topics
- "Git merge vs git rebase differences explained"
- "How and when to use git stash"
- "Git cherry-pick examples and use cases"
- "Recovering lost commits with git reflog"

---

### The Practical Challenge

**Part 1: Generating Conflicts**
1. Continue using your `git_practice` repository. Ensure you are on `main`.
2. Create and switch to a new branch: `git checkout -b experiment`.
3. Open `index.html` and edit the very first line to: `<h1>Hello Experiment</h1>`.
4. Stage and commit the change: `git commit -am "Update heading for experiment"`.
5. Switch back to your primary branch: `git checkout main`.
6. Edit the *exact same line* in `index.html` to: `<h1>Hello Main Branch</h1>`.
7. Stage and commit the change: `git commit -am "Update heading on main"`.

**Part 2: Rebasing and Resolving Conflicts**
1. Switch back to the `experiment` branch.
2. Tell Git to re-apply your experimental commit on top of the new `main` commit: 
   `git rebase main`.
3. Git will pause the rebase, warning you of a merge conflict.
4. Run `git status`. It will say `index.html` has unmerged paths.
5. Open `index.html` in an editor. You will see cryptic merge markers:
   ```html
   <<<<<<< HEAD
   <h1>Hello Main Branch</h1>
   =======
   <h1>Hello Experiment</h1>
   >>>>>>> Update heading for experiment
   ```
6. Delete the markers and choose ONE of the headings to keep. Save the file.
7. Stage the resolved file: `git add index.html`.
8. Continue the rebase process: `git rebase --continue`.
9. Your history is now perfectly linear! The `experiment` commit sits neatly on top of the `main` commit.

**Part 3: Stashing Unfinished Work**
1. While on `experiment`, add a new paragraph to `index.html`, but **do not commit it**.
2. Suddenly, you realize you need to switch to `main` to fix an emergency bug.
3. If you run `git checkout main`, Git might refuse depending on uncommitted state overlaps.
4. "Shelve" your changes temporarily: `git stash save "WIP on paragraph 3"`.
5. Run `git status`. Notice your working directory is totally clean!
6. Switch to `main`, fix your "urgent issue", and switch back to `experiment`.
7. Retrieve your unfinished work: `git stash pop`. Your paragraph reappears.

**Part 4: Cherry-picking and The Reflog**
1. While on `experiment`, create a new file `awesome_feature.txt`, commit it, and note the commit hash from `git log`.
2. Switch back to `main`.
3. Instead of merging the entire `experiment` branch, you only want that *single* file's commit.
4. Type: `git cherry-pick <your_commit_hash>`. The `awesome_feature.txt` instantly appears and is committed to `main`!
5. Now, pretend you accidentally deleted your entire branch. Type `git reflog`.
6. Notice the reflog contains a persistent timeline of absolutely every move your HEAD pointer has ever made.
7. You can travel back in time to any state by copying a hash from the reflog and running: `git reset --hard <hash>`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Never `git rebase` commits that exist on a public, shared remote branch (like GitHub). Rebasing rewrites the underlying hashes. If other developers have already pulled those commits, their history will permanently diverge from yours, causing chaos. Rebase local branches only!
- **Gotcha 2:** `git stash pop` restores the stash and simultaneously deletes it from your stash list. `git stash apply` restores it but keeps a permanent backup in the list.
- **Gotcha 3:** `git commit -am` is a fast shorthand for `git add .` + `git commit -m`. However, it only stages files that are *already tracked*. It will quietly ignore completely new files.

### Reflection Question
If `git log` only shows the history of the current branch backward through its parents, why is `git reflog` considered the ultimate "undo button" when you screw up a merge?
> *Hint: Think about what the HEAD tracks versus what branches track.*