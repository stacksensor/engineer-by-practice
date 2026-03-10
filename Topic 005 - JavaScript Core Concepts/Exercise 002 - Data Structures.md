# Exercise 002 - Data Structures (Objects/Arrays)

### Objective
Store, retrieve, and destructurally manipulate large batches of related information dynamically using JavaScript's native complex reference types.

### Core Concepts to Master
- **Arrays `[]`:** Ordered, numbered lists of data. Access relies heavily on the index location (`0, 1, 2`).
- **Objects `{}`:** Unordered dictionaries containing Key-Value pairs. Access relies purely on the string name of the Key (`user.name`).
- **Pass-By-Reference:** Primitives (numbers, strings) copy their raw *value* when assigned. Arrays/Objects copy their *memory address*.
- **Destructuring:** Modern syntactic sugar allowing you to violently rip variables instantly out of the depths of objects and arrays in a single clean line.

### Research Topics
- "JavaScript Value vs Reference types"
- "Object destructuring and Array destructuring ES6"
- "The Spread Operator in JS (...) explained"

---

### The Practical Challenge

**Part 1: The Reference Trap**
1. Create a variable `let a = 10;`. Create `let b = a;`. Re-assign `b = 50;`. Console.log both. Note that `a` is completely unaffected. Primitives are independent physical copies.
2. Now, create an object: `const playerOne = { health: 100 };`.
3. Asssign it: `const playerTwo = playerOne;`.
4. The second player takes damage: `playerTwo.health = 40;`.
5. Log `console.log(playerOne.health);` The original player one also has 40 health! Why? You didn't copy the object; you simply gave two different variable names access to the exact same physical block of RAM.

**Part 2: The Spread Operator Clone**
1. To safely copy an object without the dangerous reference link, you must physically unpack it into a new shell. 
2. Delete the `playerTwo` assignment from Part 1, and replace it with:
   `const playerTwo = { ...playerOne };`.
3. The three dots `...` (Spread Operator) physically iterated over all keys in `playerOne` and pasted pristine literal copies of them into the new empty `{}`.
4. Alter `playerTwo.health = 40;`. Log both again. `playerOne` is now safely secure at `100`.

**Part 3: Destructuring Objects**
1. Create a massive JSON-style Database payload:
   ```javascript
   const serverResponse = {
       status: 200,
       data: {
           id: 9942,
           username: "SystemCrusher",
           metadata: { lastLogin: "Tuesday", IP: "127.0.0.1" }
       }
   };
   ```
2. The old way to get the IP Address requires massive dot chaining:
   `const ip = serverResponse.data.metadata.IP;`
3. Use ES6 object destructuring to rip the exact properties you want out of the nested objects securely in one block:
   ```javascript
   const { status, data: { username, metadata: { IP } } } = serverResponse;
   console.log(status, username, IP);
   ```
4. It reads like a mirror image of the object. Try assigning the `IP` to a completely new variable name during extraction: `metadata: { IP: lastKnownAddress }`.

**Part 4: Destructuring Arrays**
1. Build an array of high scores: `const topScores = [990, 850, 420, 110];`.
2. Extract the gold and silver medalists using their orderly index positioning:
   `const [gold, silver] = topScores;`
3. Log them. Notice that array destructuring does not care about names (like objects do). It maps names sequentially slot-for-slot.
4. Extract the gold medalist, but use the `...rest` pattern to dump all remaining losers into a separate array variable:
   `const [winner, ...losers] = topScores;` 
5. Log `losers`. Notice it is a fully functioning nested array containing `[850, 420, 110]`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Destructuring a key that does not exist in an object silently returns `undefined` without crashing. To protect your app, provide a default fallback: `const { role = "Guest" } = user;`.
- **Gotcha 2:** The Spread Operator `...` ONLY performs a "Shallow Clone". If the object you are cloning contains nested dictionaries deeply inside of it, those nested dictionaries are still linked by physical reference. (Use `structuredClone(obj)` for an absolute, deep mathematical detachment).
- **Gotcha 3:** To spread an array into an object `{ ...myArray }`, the engine physically converts array indices into object keys `{ "0": 990, "1": 850 }`.

### Reflection Question
If you pass a massive `user` configuration object as an argument into a function `updateProfile(user)`, and you alter a property natively inside the function block, does that alteration permanently permanently break the original `user` object out in the global scope? Why?