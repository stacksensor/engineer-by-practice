# Exercise 003 - Editor Mastery: The Keyboard-Only Workflow

### Objective
Dance on the keys. Master **Editor Productivity**—the art of using your IDE (VS Code, Vim, Cursor) without touching your mouse for 90% of your work. Learn the core **Keyboard Shortcuts** for Multi-cursor editing, Global Search, and Symbol Navigation, and understand why the "Vim Mindset" is the fastest way to edit text.

### Core Concepts to Master
- **The Palette (CMD+SHIFT+P or CTRL+SHIFT+P):** The "Universal Search" for any command in VS Code. Never search a "Menu" again.
- **Symbol Search (CMD+SHIFT+O):** Jumping straight to a function name (e.g., `@handleLogin`) in a 1,000-line file.
- **Global Search (CMD+SHIFT+F):** Find "User" in your ENTIRE PROJECT in 0.1s.
- **Multi-cursor (CMD+D or ALT+Click):** Changing 50 lines of code at once.
- **Vim Mode:** The "Modal" editing style where `d-w` means "Delete Word" and `y-p` means "Copy Line." (The "Language" of text editing).

### Research Topics
- "VS Code shortcuts every developer should know"
- "Introduction to Vim: Why developers love the 'Hardest' editor"
- "Multi-cursor editing in VS Code: A tutorial"
- "Symbol navigation and 'Go to Definition' (F12)"

---

### The Practical Challenge

**Part 1: The "Mouse" Challenge (Scenario)**
1. You have a list of 100 constants: `CONST_A = 1`, `CONST_B = 2`, etc.
2. You want to add `export` to the start of every line.
3. **Manual (Mouse):** Click, type, repeat 100 times. (Time: 3 minutes).
4. **Multi-cursor (Keyboard):** Select `CONST`, press `CMD+D` (100 times), press `Home`, type `export `. (Time: 5 seconds).
5. Discuss: Why does this feel like a "Superpower"?

**Part 2: The "Navigation" Sprint**
1. Open a large file in your IDE.
2. Jump to line 500 without scrolling. (Answer: `CMD+G 500`).
3. Find a function named `handleAuth` without scrolling. (Answer: `CMD+SHIFT+O`).
4. Find the file `user.profile.js` without using the "Files" sidebar. (Answer: `CMD+P`).

**Part 3: The "Vim" Mindset (Concept)**
1. Research how **Vim** separates "Moving" from "Typing." 
2. Discuss: Why is the mouse much slower than the `h`, `j`, `k`, `l` keys for moving one character at a time? 
3. (Answer: Because your hands never have to leave the 'Home Row').

**Part 4: Identifying the "Shortcut"**
1. Research the shortcut for:
   - "Delete current line" (Answer: `CMD+SHIFT+K`).
   - "Comment out current line" (Answer: `CMD+/`).
   - "Move current line Up/Down" (Answer: `ALT+Up/Down`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Over-customizing. If you change 500 shortcuts, you will be "Helpless" when you use a colleague's machine or a remote server. Stick to the "Standards" as much as possible.
- **Gotcha 2:** Only knowing "One" tool. If you only know VS Code, you will be stuck when you have to edit a config file on a Linux server. Learn basic **`vim`** keys for emergencies!

### Reflection Question
Why are the "Top" developers often the ones who can write 1,000 lines of code without ever moving their hand to the mouse? (Answer: Because their hands can move just as fast as their thoughts).
