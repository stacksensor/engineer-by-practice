# Exercise 004 - Terminal Multiplexers: Tmux & Screen

### Objective
Multiply the screen. Master **Terminal Multiplexers**—the tools that allow you to split your terminal into many smaller windows AND keep your processes running even if your laptop's battery dies or you lose Wi-Fi. Learn about **Tmux** (The modern choice) and **Screen** (The classic choice) and understand how to manage "Remote Sessions."

### Core Concepts to Master
- **The Session:** A "Container" for your work. You can "Attach" and "Detach" from a session at any time.
- **The Window:** A "Tab" inside a session. 
- **The Pane:** A "Split" (Left/Right or Top/Bottom) inside a single window.
- **Detach (`CTRL-B d`):** Leaving your code running on the server while you "Logout" or go home.
- **Persistence:** Why your `npm run dev` doesn't stop just because your Wi-Fi crashed.

### Research Topics
- "Introduction to Tmux: Sessions, Windows, and Panes"
- "How to keep a script running after you logout with 'nohup' or 'tmux'"
- "Tmux vs GNU Screen: Which to choose in 2024?"
- "Customizing your .tmux.conf for maximum speed"

---

### The Practical Challenge

**Part 1: The "Split" Screen (Scenario)**
1. You want to see:
   - Your **Source Code** (Left).
   - Your **Unit Test** output (Top Right).
   - Your **Server Logs** (Bottom Right).
2. Using a standard terminal: You need 3 separate windows. (Cluttered!).
3. Using **Tmux**: `tmux split-v` and `tmux split-h`.
4. Discuss: How does this help you "Debug" a problem by seeing all 3 at once?

**Part 2: The "Persistence" Trick (Concept)**
1. Connect to a remote server with `ssh`.
2. Start a long-running script (e.g., `python train_model.py`). 
3. After 5 minutes, your Wi-Fi dies. 
4. Discuss: Did your script stop? (Answer: **Yes**, normally!).
5. How does `tmux` fix this? (Answer: If you started the script inside a `tmux session`, it keeps running on the server even if you "Disconnect"!).

**Part 3: The "Attach" Search**
1. Research the command: `tmux attach`. 
2. Discuss how it feels to "Resume" your work on a server from a completely different computer. 
3. (Answer: All your windows and panes are exactly how you left them!).

**Part 4: Identifying the command**
1. Research the "Prefix" key (usually **`CTRL-B`**).
2. Which keys for:
   - "Create a new window" (Answer: `CTRL-B c`).
   - "Split vertically" (Answer: `CTRL-B %`).
   - "Split horizontally" (Answer: `CTRL-B "`).
   - "Cycle between panes" (Answer: `CTRL-B o`).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Forgot to detach" mistake. If you just "Close" the terminal window without detaching properly, a "Zombified" tmux process might stay running forever, eating RAM on the server.
- **Gotcha 2:** The "Nesting" nightmare. If you open `tmux` inside another `tmux`, your "Prefix Keys" will conflict, and you will be trapped in a "Key-Press Hell"!

### Reflection Question
Why are "Terminal Multiplexers" essential for any developer who works on remote Linux servers? (Answer: Because long-distance internet connections are unreliable, and you don't want your work to be lost every time the Wi-Fi blips).
