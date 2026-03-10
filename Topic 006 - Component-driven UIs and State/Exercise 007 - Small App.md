# Exercise 007 - Small App (The Todo Engine)

### Objective
Synthesize all concepts learned across the UI module—Component compartmentalization, unidirectional Data Flow, Props parsing, `useState` localization, and JSX dynamic structural rendering—by constructing a fully functional standalone CRUD (Create, Read, Update, Delete) application natively from scratch.

### Core Concepts to Master
- **CRUD Operations:** Dynamically interacting with arrays immutably without corrupting the source data.
- **Form Submission Parsing:** Preventing browser page refreshes using `e.preventDefault()`.

### Research Topics
- "Lifting State Up React Docs"
- "Controlled Components React Input"
- "React handle form submit optimally"

---

### The Practical Challenge

**Part 1: The Global Architecture**
1. Scaffold a fresh Vite React app.
2. Draw the layout conceptually. You will build an `<App>` component acting as the global state dictator holding the data.
3. It will render 3 separate components:
   - `<Header>` (static text).
   - `<TodoInput>` (A form block).
   - `<TodoList>` (A list container mapping an array).
4. Each todo inside the array will be rendered using a nested `<TodoItem>` element.

**Part 2: Form Capture and Data Immutability**
1. Inside `<App>`, initialize the dictator array exactly:
   `const [todos, setTodos] = useState([{ id: 1, text: "Learn React", completed: false }]);`
2. Build the `<TodoInput>`. Give it localized state `const [text, setText] = useState("")`. Bind it to an input element (Use `value={text}` and `onChange`).
3. The `<TodoInput>` needs a way to send the payload back to `<App>`.
4. In `<App>`, define:
   ```jsx
   function addTodo(text) {
       const newTodo = { id: Date.now(), text: text, completed: false };
       setTodos([...todos, newTodo]);
   }
   ```
5. Pass `addTodo` securely down as a prop cleanly to `<TodoInput addTodo={addTodo} />`.
6. Inside `<TodoInput>`, bind an `onSubmit` perfectly to the `<form>`. Have it call `props.addTodo(text)`. Remember to use `e.preventDefault()`.

**Part 3: Rendering the Engine natively**
1. In `<App>`, pass the items via props: `<TodoList items={todos} />`.
2. Read the array properly dynamically: `function TodoList({ items }) { ... }`
3. Use `{items.map(todo => <TodoItem key={todo.id} todo={todo} />)}`.

**Part 4: The Deletion Pipeline**
1. In `<App>`, build the deletion logic:
   ```jsx
   function deleteTodo(id) {
       setTodos(todos.filter(t => t.id !== id));
   }
   ```
2. Pass `deleteTodo` down to `<TodoList />` which then passes it to `<TodoItem />`.
3. Inside the Item component, add a delete button and wire it up to call `props.deleteTodo(props.todo.id)`.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Remembering to use `e.preventDefault()` inside your `<form>` submit handler. If you forget this, clicking your "Add Todo" button will physically cause the entire React Application window to trigger an HTTP POST refresh, wiping your React state from RAM instantly.
- **Gotcha 2:** Array Immutability is the number one bug source for beginners. Doing `todos.push(newItem)` followed by `setTodos(todos)` will fail to render entirely. You MUST use the spread operator: `setTodos([...todos, newItem])`.

### Reflection Question
Why do we build `addTodo` inside the Parent `<App>` component and pass it down to `<TodoInput>`, instead of writing the logic directly inside `<TodoInput>`?