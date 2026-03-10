# Exercise 004 - Trees I (Binary Search Trees)

### Objective
Graduate from one-dimensional linear data structures into two-dimensional branched hierarchies. Master the algorithmic architecture of Binary Search Trees (BST), enabling exponential search efficiency.

### Core Concepts to Master
- **Hierarchical Data:** Unlike arrays which sequence items one after another horizontally, trees establish structural parent-to-child relationships.
- **Node Mechanics:** Every tree is built from individual isolated Nodes containing three properties: `value`, `left`, and `right`.
- **The Binary Rule:** A parent Node can physically hold exactly a maximum of two descendants.
- **The BST Sorting Rule:** All numbers structurally smaller than the parent must explicitly reside on the left branch. All numbers structurally larger must explicitly reside on the right branch.
- **O(log N) Time Complexity:** Slicing a searchable dataset essentially in half every single step.

### Research Topics
- "JavaScript implementing a basic Tree Node"
- "Binary search tree insert time complexity"
- "Traversing a binary tree graphically"

---

### The Practical Challenge

**Part 1: The Raw Node Blueprint**
1. In a Node.js file, define the absolute fundamental building block: `class Node { ... }`.
2. Construct the initialization blueprint. `this.value = data`, `this.left = null`, `this.right = null`.
3. Manually create three instances: `const root = new Node(10);`, `const childA = new Node(5);`, and `const childB = new Node(15);`.
4. Manually link them perfectly: `root.left = childA;` and `root.right = childB;`.

**Part 2: The Tree Manager Class**
1. Define the actual encompassing data structure: `class BinarySearchTree { ... }`.
2. Construct the root tracker: `this.root = null`.
3. Build the core method: `insert(data)`.
4. If `this.root` is mathematically strictly `null`, set it to the new Node completely.
5. If not null, you must traverse downwards explicitly. Create a variable `let current = this.root`.

**Part 3: The Insertion Loop**
1. Build a `while(true)` loop inside your `insert()` method.
2. Evaluate the new `data` against `current.value`.
3. If new data is mathematically identical, `return undefined` (No structural duplicates allowed in standard sets).
4. If strictly less, check if `current.left` exists. If not, assign the new Node to `current.left` and cleanly `return this`. Otherwise, re-assign `current = current.left` to travel structurally deeper.
5. Mirror the logic mathematically identically for the right descendant side.

**Part 4: The Rapid Search Method**
1. Build a `find(data)` method cleanly.
2. If `root` is null, explicitly `return false`.
3. Set `let current = this.root` and build a second `while` loop that structurally terminates `while(current)` exists.
4. If `data < current.value`, move the pointer `current = current.left`.
5. If `data > current.value`, move the pointer `current = current.right`.
6. If the explicit match is mathematically identical, explicitly return the entire `current` Node physically.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** A wildly unbalanced tree behaves identically computationally to a sluggish Linked List array natively. If you sequentially insert `[1, 2, 3, 4, 5, 6, 7]`, the BST will mathematically degenerate into a single massive right-leaning diagonal branch natively. The O(log N) efficiency is fundamentally destroyed cleanly. (Advanced trees use auto-balancing mechanisms like AVL or Red-Black architectures).
- **Gotcha 2:** Junior developers frequently accidentally break their traversal loops by forgetting to mathematically reassign the `current` variable physically deeper, creating an infinite locked loop that freezes the Node server entirely.

### Reflection Question
If you have a perfectly mathematically balanced binary tree containing exactly 1,000,000 numerical records structurally, what is the absolute maximum structural depth (or worst-case number of step comparisons) required to natively locate a single specific integer mathematically?