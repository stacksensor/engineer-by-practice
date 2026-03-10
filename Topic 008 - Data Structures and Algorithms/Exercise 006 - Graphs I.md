# Exercise 006 - Graphs I (Adjacency Matrix & List)

### Objective
Learn the fundamentals of Graph theory. Map non-linear relational data where nodes can connect to any other node without strict hierarchical restrictions.

### Core Concepts to Master
- **Vertices and Edges:** The Graph terminology for "Nodes" and "Connections".
- **Directed vs Undirected:** Connections that travel one way (like Twitter followers) versus two-way streets (like Facebook friends).
- **Adjacency Matrix:** A 2D array storing boolean indicators of node connections.
- **Adjacency List:** An object map storing arrays of connected nodes for every vertex.

### Research Topics
- "Graph data structure JavaScript"
- "Adjacency Matrix vs Adjacency List"
- "Real world representations of undirected graphs"

---

### The Practical Challenge

**Part 1: The Adjacency Matrix**
1. Define a 5x5 Matrix (an array containing 5 arrays).
2. Use `1` to indicate a physical connection and `0` to indicate no connection.
3. Map an undirected graph. If node A connects to Node B, ensure Node B also connects back to Node A inside the matrix structure.

**Part 2: The Graph Class and Adjacency List**
1. Create a `class Graph { ... }`.
2. Construct the underlying structure using an empty JavaScript Map or Object `this.adjacencyList = {}`.
3. Build the method `addVertex(node)`. It should initiate a new array associated with the node key.

**Part 3: Establishing Edges**
1. Design `addEdge(node1, node2)`.
2. Inside the method, locate the array for `node1` and push `node2` into it.
3. Locate the array for `node2` and push `node1` into it.
4. Test your logic by creating a map of standard cities (e.g., "Seattle", "Los Angeles") and connecting them.

**Part 4: Severing Connections**
1. Create `removeEdge(node1, node2)`.
2. Filter the array inside `node1` to remove `node2`.
3. Filter the array inside `node2` to remove `node1`.
4. Create `removeVertex(node)`. It must loop through every single adjacent node before deleting the primary node to prevent ghost references.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Adjacency Matrices waste immense memory storing `0`s for disconnected nodes. Use them only when graphs are extremely dense.
- **Gotcha 2:** Undirected graphs duplicate connection data explicitly. Always update both vertices concurrently when adding or removing edges.

### Reflection Question
Why are social media networks optimally stored as Adjacency Lists instead of Matrices?