# Exercise 005 - Trees II (Traversal & Tries)

### Objective
Master complex tree traversal algorithms (BFS and DFS) to map hierarchical data. Construct specialized String Tries for search engine auto-completion behavior.

### Core Concepts to Master
- **Breadth-First Search (BFS):** Scanning the tree horizontally level by level.
- **Depth-First Search (DFS):** Plunging down an isolated vertical branch to the bottom leaf before backtracking.
- **The Call Stack Recursion:** How DFS utilizes the internal JavaScript engine stack to auto-resume branch traversal.
- **Trie (Prefix Tree):** An advanced non-binary N-ary tree structured explicitly to store text prefixes.

### Research Topics
- "JavaScript BFS vs DFS differences"
- "DFS Preorder, Inorder, Postorder explained"
- "How does a Trie data structure work for autocomplete"

---

### The Practical Challenge

**Part 1: The Breadth-First Search**
1. Open the `BinarySearchTree` class from Exercise 004.
2. Build a new instance method: `BFS()`.
3. Construct two arrays: `let queue = []` and `let data = []`.
4. Define a tracker `let node = this.root` and manually `push(node)` into the `queue`.
5. Write an explicit loop: `while (queue.length)`.
6. `shift()` the first item out of the queue, push its `value` into the `data` array.
7. If the node mathematically contains a `left` child, `push` it onto the `queue`. Mirror for the `right` child.

**Part 2: The Depth-First Search Recursion**
1. Build another explicit instance method: `DFSPreOrder()`.
2. Construct one array: `let data = []`.
3. Write a localized nested helper recursive function: `function traverse(node)`.
4. Inside `traverse()`, push `node.value` directly into `data`.
5. If `node.left` exists, invoke `traverse(node.left)`.
6. Provide identical logic for the right side.

**Part 3: Understanding Trie Mechanics**
1. Implement a distinct structural data model explicitly for string text mapping.
2. Tries do not store full strings locally. Each Trie node holds a Map housing single alphabetical letters.
3. Store standard letter objects inside each Trie node.

**Part 4: Implementing Auto-Complete**
1. Construct algorithms extracting data from the Trie.
2. Ensure the node implementation searches and returns valid complete words specifically based on provided string prefixes.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Accidentally altering the physical structural tree hierarchy during traversal. Always isolate reads from writes.
- **Gotcha 2:** Deep recursion throws Stack Overflow trace exceptions. Ensure your base cases are absolute.

### Reflection Question
If an array explicitly consumes excessive memory storing repeating strings, in what context does a Trie definitively save computational RAM?