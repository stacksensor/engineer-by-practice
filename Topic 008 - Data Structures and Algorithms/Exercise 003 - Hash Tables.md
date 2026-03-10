# Exercise 003 - Hash Tables

### Objective
Comprehend the fundamental architecture behind JavaScript Objects and Maps. Build a raw Hash Table algorithm from scratch to mathematically map text strings to explicit physical memory addresses instantaneously.

### Core Concepts to Master
- **The Hashing Algorithm:** A mathematical function that inputs a variable-length string and outputs a fixed-length deterministic integer.
- **O(1) Data Retrieval:** How Hash Tables achieve instant data lookups without scanning the entire array.
- **Hash Collisions:** When two completely different strings mathematically compute to the same exact integer address, and how to resolve the memory overlap.
- **Buckets:** The underlying memory grid that stores the physical data payloads.

### Research Topics
- "How do hash tables work"
- "Understanding hash collision resolution (Separate Chaining)"
- "Creating a simple string hashing function in JavaScript"

---

### The Practical Challenge

**Part 1: The Hashing Algorithm**
1. Open a blank Node file and write a function named `hashStringToInt(string, tableSize)`.
2. Initialize a local variable `hash = 17`.
3. Loop through every character in the string. For each character, multiply the `hash` by a generic prime number (like 13) and add the character's ASCII code (`charCodeAt(0)`).
4. Return `hash % tableSize` as the absolute final integer. 
5. Test it: `hashStringToInt("Sujit", 50)` should consistently output the exact same integer between 0 and 49 every time you run it.

**Part 2: The Hash Table Class**
1. Define a robust structural class `class HashTable`.
2. In the constructor, initialize `this.table` as a brand new `Array(50)`.
3. Build the `setItem(key, value)` method.
4. When `setItem` is called, run `key` through your hashing algorithm to find the exact array index.
5. Store the `value` directly in the array at that specific computed index.

**Part 3: Retrieving Data instantly**
1. Build the corresponding `getItem(key)` method.
2. Hash the `key` again. This mathematically guarantees you get the exact integer where the data was saved.
3. Access `this.table[computedIndex]` directly and return it.
4. You have successfully bypassed looping linear arrays. You can look up a value instantly in O(1) time.

**Part 4: Handling Collisions explicitly**
1. Your algorithm currently has a fatal structural flaw. What happens if the string `"Apple"` and the string `"Orange"` both mathematically hash to the index of `24`? The second item will permanently overwrite the first.
2. Refactor `setItem`. Instead of storing the value directly as a string, store it as an inner Array (a Bucket).
3. If `index 24` is empty, insert `[["Apple", 5]]`. 
4. If `index 24` already contains data, push the new data into the existing bucket: `[["Apple", 5], ["Orange", 8]]`.
5. Refactor `getItem` to loop specifically through the isolated mini-array at the hashed index to correctly return the distinct data payload.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Junior developers forget that JavaScript standard `{}` Objects are literally just Hash Tables natively under the hood. All string keys are hashed by the V8 Engine directly into C++ memory allocations.
- **Gotcha 2:** Poorly optimized hash algorithms create terrible distribution grids, resulting in 90% of strings colliding within the exact same index bucket. This fundamentally degrades your supposedly instant O(1) architecture back to a sluggish O(N) array search.

### Reflection Question
If raw Arrays are significantly faster to write loops for, under what exact architectural condition does storing 10,000 user records inside a Hash Map completely destroy an Array in CPU execution speed?