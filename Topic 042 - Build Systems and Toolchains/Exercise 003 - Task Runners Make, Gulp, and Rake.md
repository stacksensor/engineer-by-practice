# Exercise 003 - Task Runners: Make, Gulp & Rake

### Objective
Automate the ritual. Master **Task Runners**—the scripts and tools that allow you to say one word (e.g., `make build`) and have the computer perform 10 different actions in the right order. Learn how to define **Dependencies** between tasks (e.g., "Don't 'Deploy' unless the 'Tests' have finished successfully") and understand why a "Task Runner" is the brain of your Build System.

### Core Concepts to Master
- **The Task:** A single command (e.g., "Run the tests").
- **The Dependency:** Task B "requires" Task A. (e.g., `deploy` depends on `build`).
- **NPM Scripts:** Using `package.json` as a task runner. (The modern web choice).
- **Makefile (Again):** Using `make` to run generic scripts (The old school robust choice).
- **Rake (Ruby):** The task runner for the Ruby/Rails world.
- **Incremental Tasks:** "Only run this task if the input files are newer than the output files."

### Research Topics
- "Task Runners vs Build Systems: Are they the same?"
- "How to define dependencies in a Makefile"
- "Using 'Gulp' or 'Grunt' for complex asset pipelines"
- "Running tasks in parallel for speed"

---

### The Practical Challenge

**Part 1: The "Manual" Ritual (Scenario)**
1. To deploy your app, you must:
   - Run `pytest`.
   - Run `eslint`.
   - Run `docker build`.
   - Run `docker push`.
2. Discuss the 3 things that go wrong if you do this manually:
   - (Answer: 1. You forget a step. 2. You do them in the wrong order. 3. You push the code even if the tests failed!).

**Part 2: The "NPM Script" Fix**
1. Add a `scripts` section to your `package.json`: 
   - `"test": "jest"`
   - `"predeploy": "npm test"`
   - `"deploy": "sh deploy.sh"`
2. Type `npm run deploy`. 
3. Observe how it runs the "test" first automatically.

**Part 3: The "Make" Target (Concept)**
1. Write a `Makefile` with a target: 
   - `build: file1.c file2.c \n gcc file1.c file2.c -o out`.
2. Discuss: If you run `make build` and then run it again *without changing the files*, does it compile again? 
3. (Answer: No! `make` is smart enough to know nothing changed).

**Part 4: Identifying the "Runner"**
1. Which runner for:
   - "A Rails app" (Answer: Rake).
   - "A React app" (Answer: NPM Scripts).
   - "A C++ project" (Answer: Make / CMake).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Hidden Dependencies. If Task B depends on Task A, but you don't declare it in the file, Task B will eventually fail intermittently because Task A hasn't finished yet.
- **Gotcha 2:** "Shell Hell." Writing long, complex bash scripts inside a JSON file or Makefile is a nightmare to debug. Put complex logic in a separate script (like `scripts/deploy.sh`) and call THAT from the runner.

### Reflection Question
Why are "Task Runners" better than "Bash Scripts" for complex builds? (Answer: Because task runners understand 'Dependencies' and 'Parallelism' automatically, while bash scripts just run one line after another).
