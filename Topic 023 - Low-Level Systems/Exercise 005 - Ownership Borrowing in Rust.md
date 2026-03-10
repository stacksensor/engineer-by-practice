# Exercise 005 - Ownership & Borrowing in Rust

### Objective
Master the "Rules of the Cluster." Learn the three fundamental rules of **Ownership** in Rust that allow it to manage memory without a garbage collector. Understand **Borrowing** (References) and **Lifetimes**, and learn how to navigate the "Borrow Checker" to write safe, efficient code.

### Core Concepts to Master
- **The 3 Rules of Ownership:**
  1. Each value in Rust has a variable called its **Owner**.
  2. There can only be **one owner** at a time.
  3. When the owner goes out of scope, the value is **dropped** (deleted from memory).
- **Move semantics:** Passing a value to a function "Moves" ownership, making the original variable invalid.
- **Borrowing (`&`):** Passing a "Reference" to a value so a function can read it without taking ownership.
  - **Shared Borrowing (`&T`):** Any number of readers.
  - **Mutable Borrowing (`&mut T`):** Exactly ONE writer at a time, and NO readers.

### Research Topics
- "The Rust Ownership rules explained"
- "Moving vs Borrowing in Rust"
- "The most common Borrow Checker errors and how to fix them"

---

### The Practical Challenge

**Part 1: The "Move" error**
1. Write this code in a Rust file:
   ```rust
   let s1 = String::from("hello");
   let s2 = s1;
   println!("{}", s1); // This will fail!
   ```
2. Run `cargo run`. Observe that the compiler says "Value used here after move."
3. Explain why Rust does this. (Hint: If `s1` and `s2` both owned the same heap memory, they would both try to delete it when they go out of scope, causing a "Double Free" crash).

**Part 2: Borrowing to the Rescue**
1. Fix the error by using a Reference: `let s2 = &s1;`.
2. Observe how `println!("{}", s1);` now works because `s2` is just "Borrowing" the data, not taking ownership.

**Part 3: The Write Rule (Mutable Borrowing)**
1. Try to have two mutable references to the same data:
   ```rust
   let mut x = 10;
   let r1 = &mut x;
   let r2 = &mut x;
   r1 = 20; // This will fail!
   ```
2. Research why Rust forbids having two writers (or a writer and a reader) at the same time. (Hint: It prevents "Data Races").

**Part 4: Visualizing the "Drop"**
1. Create a variable inside an inner scope `{ ... }`.
2. Try to access it outside that scope. 
3. Observe the "Out of scope" error. This is how Rust automatically cleans up the Heap without a Garbage Collector.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The `Clone` escape hatch. If you really need a copy of the data, use `.clone()`. But be careful—cloning the heap is expensive! Try to "Borrow" whenever possible.
- **Gotcha 2:** Dangling References. Rust prevents you from returning a reference to a variable that was created *inside* the function (because the variable will be dropped, leaving the reference pointing at nothing).

### Reflection Question
How does Rust's rule of "One Owner" eliminate the possibility of a "Use-After-Free" memory bug?
