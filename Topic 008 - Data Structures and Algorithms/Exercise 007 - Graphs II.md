# Exercise 007 - Graphs II (Dijkstra's Algorithm)

### Objective
Master Pathfinding. Implement Dijkstra's Algorithm to compute the shortest route between two specific nodes on a weighted graph, emulating GPS navigation fundamentals.

### Core Concepts to Master
- **Weighted Edges:** Establishing relational graphs where the connections store numerical costs (distance, time, or friction).
- **The Priority Queue:** A data structure used to efficiently sort and fetch the minimum numerical value first.
- **Shortest Path Trees:** Data structures used to store the absolute minimum calculated distance to each node from a starting vertex.
- **Greedy Algorithms:** Algorithms that make decisions based on the best local option available at each step.

### Research Topics
- "Dijkstra algorithm JavaScript"
- "Implementing basic Priority Queue array"
- "Weighted graph data structures"

---

### The Practical Challenge

**Part 1: The Weighted Graph**
1. Extend the Graph class built in Exercise 006.
2. Update the `addEdge(node1, node2, weight)` signature to expect a numerical cost.
3. Modify the adjacency list to store objects: `{ node: "Destination", weight: 500 }`.
4. Ensure the push operation is mirrored if the graph is undirected.

**Part 2: The Priority Queue Scaffold**
1. Build a barebones `PriorityQueue` class.
2. initialize an array: `this.values = []`.
3. Implement `enqueue(val, priority)`. It should push the object and then sort the array to keep the lowest priority value at index 0.
4. Implement `dequeue()`. It should return the value with the highest priority (lowest numerical value) and remove it from the array.

**Part 3: The Distance Table**
1. Define the main method: `Dijkstra(startNode, endNode)`.
2. Initialize three helper structures:
   - `distances`: A map where every node starts with a value of `Infinity`, except the `startNode` which starts at `0`.
   - `previous`: An object mapping each node to the node that preceded it in the shortest path.
   - `queue`: An instance of your PriorityQueue to track which nodes to evaluate next.

**Part 4: The Core Pathfinding Loop**
1. Enqueue the `startNode` with a priority of `0`.
2. Run a loop while the queue contains values.
3. Dequeue the node with the smallest distance. If it is the `endNode`, reconstruct the path and return it.
4. Otherwise, iterate through its neighbors. Calculate the total distance from the start node to each neighbor.
5. If the new distance is smaller than the previously stored distance, update the `distances` map and the `previous` tracker, and enqueue the neighbor.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Initialization Errors. Ensure every node in the graph is initialized in the `distances` map. Comparing a number against `undefined` will break the greedy logic.
- **Gotcha 2:** Negative Weights. Dijkstra's algorithm cannot handle negative graph edges. If your graph contains negative costs, you must investigate the Bellman-Ford algorithm.

### Reflection Question
Why does using a simple array instead of a Priority Queue significantly degrade the time complexity of Dijkstra's algorithm?