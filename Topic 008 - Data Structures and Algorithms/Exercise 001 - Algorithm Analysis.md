# Exercise 001 - Algorithm Analysis

### Objective
Master Big O Notation. Transition from writing code that "just works" to writing mathematical logic that scales efficiently even when processing datasets of ten million records.

### Core Concepts to Master
- **Time Complexity (Big O):** A standardized mathematical categorization describing how an algorithm's runtime grows as the input data `N` geometrically increases.
- **O(1) - Constant Time:** The operation executes instantly, regardless of whether the array has 5 items or 5 billion items (e.g., `array[index]`).
- **O(N) - Linear Time:** The algorithm must physically process every single item in the data structure consecutively (e.g., standard `for...loop` or `.find()`).
- **O(N²) - Quadratic Time:** Nested linear loops. It triggers exponentially worse performance as data grows (e.g., comparing every item against every other item).

### Research Topics
- "Big O notation explained simply"
- "Time vs Space complexity tradeoffs"
- "JavaScript array method time complexities"

---

### The Practical Challenge

**Part 1: The O(N) Benchmark**
1. Open a blank Node.js file. Generate an immense physical array of exactly `5,000,000` integers.
2. Manually push a specific target number `999` into the very last slot.
3. Write a standard `for` loop to search for `999`.
4. Wrap the loop in `console.time("Linear")` and `console.timeEnd("Linear")` to benchmark the CPU execution strictly.
5. Run the file. Observe it taking a few milliseconds to physically read all 5,000,000 items sequentially.

**Part 2: The O(N²) Nightmare Scenario**
1. Write a function that finds duplicate numbers in a generic array.
2. Implement it using nested `for` loops explicitly:
   ```javascript
   for (let i = 0; i < array.length; i++) {
       for (let j = 0; j < array.length; j++) {
           if (i !== j && array[i] === array[j]) return true;
       }
   }
   ```
3. Pass your `5,000,000` integer array perfectly into this exact function.
4. Attempt to run the benchmark. The Node process will practically freeze your terminal. It is computationally attempting exactly 25 Trillion individual physical operations.

**Part 3: The O(N) Optimization**
1. Rewrite the exact duplicate-finding logic to strictly avoid nested loops entirely.
2. Declare an empty `Set` memory object explicitly before the loop.
3. Use a single standard O(N) linear `for` loop. Check if the Set contains the current integer. If `false`, `.add()` it. If `true`, you found the duplicate.
4. Pass the `5,000,000` array in. Benchmark it. It will finish perfectly in milliseconds.
5. You mathematically optimized a 25-Trillion operation O(N²) algorithm directly down to 5-Million operations O(N) by slightly increasing RAM Space Complexity.

**Part 4: Calculating Math Complexity**
1. Review built-in Array methods stringently. Evaluate `Array.prototype.push()` natively. It simply drops an item at the exact end of physical memory. This is O(1) Constant Time.
2. Evaluate `Array.prototype.unshift()`. It securely wedges an item securely at index `0`. Because memory is strictly geometric, the CPU is mathematically forced to dynamically re-index entirely every single subsequent element mechanically. Thus, `unshift()` is secretly a massive O(N) operation heavily disguised as a single function.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Assuming built-in JS methods are always O(1). Functions like `.splice()`, `.slice()`, `.indexOf()`, `.map()`, and `.filter()` all run O(N) iterations under the hood natively.
- **Gotcha 2:** Ignoring Space Complexity completely. Your O(N) Set optimization actively sacrificed RAM safely to reduce CPU runtime. This is the ultimate law of computer architecture: you must continually trade Memory Space exactly for CPU Time.

### Reflection Question
If `Array.prototype.shift()` physically removes the absolute first element in a standard array precisely, why is it structurally significantly slower computationally than dynamically calling `Array.prototype.pop()` on exactly 10 million distinct records?