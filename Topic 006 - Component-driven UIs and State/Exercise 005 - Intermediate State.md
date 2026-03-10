# Exercise 005 - Intermediate State (useReducer)

### Objective
Graduate from simple string/number `useState` variables. Securely construct complex Object trees and scale rigid business logic safely using the explicit Action-Dispatcher-Reducer architectural paradigm.

### Core Concepts to Master
- **Global State vs Local State:** Tracking exactly what data belongs where internally.
- **The Reducer Function:** A pure rigid mathematical algorithm explicitly taking an exact `(Current State, Action)` payload to physically return exclusively the `(New State)` object.
- **The Dispatcher Payload:** Formatting structural Intent events cross logic gaps accurately.

### Research Topics
- "React useReducer vs useState"
- "Redux pattern reducer action dispatch"
- "JavaScript immutable object updates"

---

### The Practical Challenge

**Part 1: The Spaghetti Trap**
1. Construct a complex `ShoppingCart.jsx` interface structurally.
2. Build 5 distinct `useState` instances explicitly: `cartTotal`, `items`, `discount`, `taxRate`, `checkoutStatus`.
3. Construct a specific function mapping exactly what happens when a User manually clicks "Remove Item":
   ```jsx
   function handleRemove(id) {
       // Filter items
       const newItems = items.filter(i => i.id !== id);
       setItems(newItems);
       // Recalculate cost logically
       const newTotal = newItems.reduce((acc, item) => acc + item.price, 0);
       setCartTotal(newTotal);
       // Remove free shipping discount precisely globally
       if (newTotal < 50) setDiscount(0);
   }
   ```
4. Imagine calculating math for "Apply Coupon", "Add Item", and "Checkout". You are desperately manually coordinating 5 unrelated distinct state setters perfectly conditionally natively. This leads to untraceable bugs.

**Part 2: Defining the Reducer Logic**
1. Abstract all data logic completely physically outside of your component natively.
2. Architect an initial data layout:
   `const initialState = { items: [], total: 0, discount: 0 };`
3. Design a `reducer` Switch/Case matrix conditionally taking external payloads explicitly:
   ```javascript
   function cartReducer(state, action) {
       switch (action.type) {
           case "ADD_ITEM":
               return { ...state, items: [...state.items, action.payload] };
           case "APPLY_COUPON":
               return { ...state, discount: 15 };
           default:
               throw new Error("Unknown action.");
       }
   }
   ```
4. Observe how this pure function specifically mathematically definitively maps logic transitions autonomously.

**Part 3: Binding the Engine**
1. Back identically structurally internally inside your physical React component, connect the native Hook rigorously:
   `const [state, dispatch] = useReducer(cartReducer, initialState);`
2. You successfully securely entirely abolished the 5 messy localized setters physically.

**Part 4: Transmitting Dispatches**
1. Update your UI buttons to intelligently format payloads directly to the Reducer precisely accurately structurally natively.
2. For adding an item logically natively:
   ```jsx
   <button onClick={() => dispatch({ type: "ADD_ITEM", payload: productData })}>
       Add to Cart
   </button>
   ```
3. Your component now strictly renders the `state.items` collection gracefully.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** A `Reducer` function must return a brand new cloned object. If you mutate the `state` object directly (e.g., `state.total = 100`), React will fail to detect the change and won't re-render.
- **Gotcha 2:** It is complete overkill to convert a simple boolean toggle into a complex `useReducer` block. Limit `useReducer` to complex data structures or interconnected logic matrices.

### Reflection Question
Why will attempting to conditionally wrap a React Hook inside an `if` block (e.g., `if (true) { useEffect(...) }`) cause your application to crash?