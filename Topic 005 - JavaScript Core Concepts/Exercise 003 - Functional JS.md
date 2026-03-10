# Exercise 003 - Functional JS (Map, Filter, Reduce)

### Objective
Eliminate standard `for (let i = 0...)` loops entirely. Master declarative, immutable array operations that transform and filter massive datasets by applying mathematical callback functions element-by-element natively.

### Core Concepts to Master
- **Callbacks:** A function passed identically as an argument into another function to be executed later.
- **`.map()`:** Iterate over an array, apply an algorithmic change to every single item, and return a perfectly identically-sized *new* array.
- **`.filter()`:** Iterate over an array, apply a boolean true/false test to every item. True items survive into the new array; false items are purged.
- **`.reduce()`:** Iterate over an array, continuously passing an "Accumulator" mathematical variable downward to crunch a list of numbers/objects down into a single definitive end value (like a total sum).
- **Immutability:** Recognizing that none of these three methods ever alter the original source array.

### Research Topics
- "JavaScript Arrow Functions syntax"
- "Difference between map and forEach JS"
- "JavaScript array filter method examples"
- "Understanding JS Array Reduce accumulator"

---

### The Practical Challenge

**Part 1: The `map` Transformation**
1. Start a script and declare a list of raw transaction amount values: 
   `const transactions = [100, -50, 400, -120];`
2. You need an array where these raw numbers are formatted as USD strings. Add a `.map()` utilizing an arrow function:
   `const formatted = transactions.map(amount => "$" + amount.toFixed(2));`
3. Console log the `formatted` array. See how it cleanly restructured the math without a single `for` wrapper.
4. Log the original `transactions` array immediately after it to prove that the immutable source data was radically untouched.

**Part 2: The `filter` Purge**
1. The accounting team only wants to see Deposits (positive numbers).
2. Create a massive chained logic block! First, hook `.filter()` straight onto the raw array to execute a boolean test:
   `const deposits = transactions.filter(amount => amount > 0);`
3. Notice how your arrow function automatically returned `true` or `false` because there are no `{}` bounding boxes requiring the explicit `return` keyword syntactic sugar.
4. Chain a `.map()` natively right onto the end of the filter algorithm:
   `transactions.filter(amount => amount > 0).map(amount => "Deposit: $" + amount);`
5. Log the pristine output.

**Part 3: The `reduce` Crunch**
1. The accounting team now needs the final standing Account Balance (the sum of all deposits minus all withdrawals).
2. Rather than mapping or filtering, use `.reduce()`. The arrow function heavily requires TWO arguments now: The `total` (accumulator) and the current `amount`.
   ```javascript
   const finalBalance = transactions.reduce((total, amount) => {
       return total + amount;
   }, 0); // Important: Providing 0 as the mathematical starting point!
   ```
3. Run the code. Observe it loops 4 times, continuously updating the internal RAM `total` value, and spits out `330` at the very end.

**Part 4: Advanced Array of Objects**
1. Load a mock database table:
   ```javascript
   const users = [
       { id: 1, name: "Alice", active: true, age: 25 },
       { id: 2, name: "Bob", active: false, age: 40 },
       { id: 3, name: "Charlie", active: true, age: 31 }
   ];
   ```
2. In a single chained variable declaration, generate an array containing **only the Names** of the users who are currently **active**.
3. *Step A:* Run a `.filter()` to eradicate Bob (check `u.active`).
4. *Step B:* Chain a `.map()` onto that specific result to destroy the object wrappers and return exclusively `u.name`.
5. Your final log should strictly print `[ "Alice", "Charlie" ]`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Junior developers routinely confuse `.forEach()` with `.map()`. `.forEach()` is a hollow loop. It executes code but returns absolutely `undefined`. `.map()` is a structural constructor. It calculates values and strictly returns a brand new Array you can natively store inside a variable.
- **Gotcha 2:** The Arrow Function syntax `x => x * 2` contains an "Implicit Return". The exact millisecond you wrap the function in curly braces `x => { x * 2 }`, it loses the implicit return and outputs `undefined` endlessly. If you use Braces, you MUST type the literal word `return x * 2`.
- **Gotcha 3:** Attempting to `reduce` an array of Objects without providing a starting Accumulator value (like `0` or `{}`) mathematically causes the `total` parameter to physically ingest the entire first *Object* instead of a number, crashing your string concatenation.

### Reflection Question
If `.map()`, `.filter()`, and `.reduce()` mathematically loop over the array entirely natively behind the scenes in the C++ V8 engine, why is replacing your manual `for (let i...)` loops with these Functional methods universally considered dramatically safer for large engineering teams?