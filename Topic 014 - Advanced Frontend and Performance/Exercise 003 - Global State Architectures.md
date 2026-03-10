# Exercise 003 - Global State Architectures

### Objective
Scale your data management. Move beyond `useState` to explore robust global state management patterns using libraries like Redux Toolkit or Zustand. Learn how to architect predictable data flows for complex, multi-page applications.

### Core Concepts to Master
- **The Store:** A single, centralized source of truth for your entire application's state.
- **Actions & Reducers:** The "Unidirectional Data Flow" pattern where data is updated through explicit events and pure functions.
- **Selectors:** Efficiently reading specific slices of the global state to minimize unnecessary component re-renders.
- **Slices (Redux Toolkit):** Organizing logic by feature (e.g., `userSlice.js`, `cartSlice.js`) rather than by technical layer.
- **Middleware (Thunks):** Handling asynchronous logic (like API calls) within the global state lifecycle.

### Research Topics
- "Zustand vs Redux Toolkit 2024"
- "Immer.js explained (how Redux handles immutability)"
- "Using createAsyncThunk for API calls"
- "When is global state necessary?"

---

### The Practical Challenge

**Part 1: The Zustand Minimalist**
1. Install Zustand: `npm install zustand`.
2. Create a "Shopping Cart" store:
   ```javascript
   const useCartStore = create((set) => ({
     items: [],
     addItem: (item) => set((state) => ({ items: [...state.items, item] })),
     clearCart: () => set({ items: [] })
   }));
   ```
3. Use this store in two separate components: An `ItemList` component that adds items, and a `Navbar` component that displays the total item count.
4. Observe how the state is shared instantly without any `Provider` wrapper.

**Part 2: The Redux Toolkit Engine**
1. Switch to a Redux architecture. Install `@reduxjs/toolkit` and `react-redux`.
2. Define an `authSlice` to handle user login/logout.
3. Configure the store and wrap your `App` in a `<Provider>`.
4. Use `useSelector` to check if a user is logged in, and `useDispatch` to trigger the login action.
5. Notice the boilerplate difference compared to Zustand.

**Part 3: Handling Async with Thunks**
1. Expand your Redux slice to fetch data from a public API (e.g., `/products`).
2. Use `createAsyncThunk` to manage the "pending", "fulfilled", and "rejected" states.
3. Observe how the UI automatically shows a loading spinner during the `pending` state and the data once `fulfilled`.
4. Implement error handling for the `rejected` state.

**Part 4: State Debugging**
1. Install the "Redux DevTools" browser extension.
2. Visit your application and perform several actions (log in, add to cart).
3. Use the extension to "Time Travel" through your state history. Watch the UI revert to previous states as you step through the actions.
4. This transparency is the primary reason for Redux's dominance in complex architectures.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Mutating State. In traditional Redux, modifying `state.items.push(x)` directly is a catastrophic error because it breaks the "Immutability" rule. Redux Toolkit includes **Immer**, which allows you to "write" mutations that are safely converted to immutable updates behind the scenes.
- **Gotcha 2:** Globalizing Everything. Do not put temporary form state (like an input value) into the Global Store. If it's only used by one component, keep it in `useState`. Global state is for data used by multiple independent branches of the UI.

### Reflection Question
Why is the "Action -> Reducer -> Store" pattern considered more predictable and easier to debug than simply using a global object that any component can modify at will?
