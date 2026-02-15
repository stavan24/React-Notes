# 🧠 Redux Toolkit Crash Course — Full Notes & Project

> 📘 Redux Toolkit Explained from Zero  
> 🚀 Includes Full Working Project  
> ⚛️ Beginner → Advanced + Interview Ready

---

## 📌 What Is Redux Toolkit?

Redux Toolkit (RTK) is the **official, recommended way to write Redux logic**.  
It solves all React Redux problems:

✔ Boilerplate elimination  
✔ Automatic immutability  
✔ Built-in best practices  
✔ Excellent developer experience

Redux Toolkit replaces older Redux setups like:

```jsx
createStore()
combineReducers()
switch statements
```

With modern APIs like:

```jsx
configureStore()
createSlice()
createAsyncThunk()
```

---

## ❓ Why Not Normal Redux?

Normal Redux has problems:

❌ Too much setup  
❌ Lots of boilerplate  
❌ Hard to scale  
❌ Hard for beginners

Redux Toolkit makes Redux:

✔ Simple  
✔ Short  
✔ Predictable  
✔ Best practice out of the box

---

## 🧠 Core Concepts

### 1️⃣ Store  
Where global state lives.

### 2️⃣ Slice  
Piece of state + reducers + actions.

### 3️⃣ Actions  
What changes state.

### 4️⃣ Reducers  
How state changes.

### 5️⃣ Async Logic  
API calls with `createAsyncThunk`

---

## 📦 Project: Simple Todo App with Redux Toolkit

### ✔ Features
- Add todo
- Toggle complete
- Remove todo
- Persist in Redux state
- Simple UI

---

## 📁 Folder Structure

```
src/
 ├── app/
 │   └── store.js
 ├── features/
 │   └── todos/
 │       ├── todoSlice.js
 │       ├── TodoInput.jsx
 │       ├── TodoList.jsx
 │       ├── TodoItem.jsx
 ├── App.jsx
 ├── main.jsx
 ├── index.css
 └── App.css
```

---

## 🛠 Redux Store — store.js

```jsx
import { configureStore } from "@reduxjs/toolkit";
import todoReducer from "../features/todos/todoSlice";

export const store = configureStore({
  reducer: {
    todos: todoReducer,
  },
});
```

---

## 🧱 Slice File — todoSlice.js

```jsx
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  items: [],
};

const todoSlice = createSlice({
  name: "todos",
  initialState,
  reducers: {
    addTodo: (state, action) => {
      state.items.push({ id: Date.now(), text: action.payload, completed: false });
    },
    toggleTodo: (state, action) => {
      const todo = state.items.find((t) => t.id === action.payload);
      if (todo) todo.completed = !todo.completed;
    },
    removeTodo: (state, action) => {
      state.items = state.items.filter((t) => t.id !== action.payload);
    },
  },
});

export const { addTodo, toggleTodo, removeTodo } = todoSlice.actions;
export default todoSlice.reducer;
```

---

## 🧾 TodoInput.jsx

```jsx
import { useState } from "react";
import { useDispatch } from "react-redux";
import { addTodo } from "./todoSlice";

function TodoInput() {
  const [text, setText] = useState("");
  const dispatch = useDispatch();

  function handleAdd() {
    if (text.trim() === "") return;
    dispatch(addTodo(text));
    setText("");
  }

  return (
    <div className="todo-input">
      <input
        placeholder="Enter task..."
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={handleAdd}>Add</button>
    </div>
  );
}

export default TodoInput;
```

---

## 🧾 TodoList.jsx

```jsx
import { useSelector } from "react-redux";
import TodoItem from "./TodoItem";

function TodoList() {
  const todos = useSelector((state) => state.todos.items);

  return (
    <div className="todo-list">
      {todos.map((todo) => (
        <TodoItem key={todo.id} todo={todo} />
      ))}
    </div>
  );
}

export default TodoList;
```

---

## 🧾 TodoItem.jsx

```jsx
import { useDispatch } from "react-redux";
import { toggleTodo, removeTodo } from "./todoSlice";

function TodoItem({ todo }) {
  const dispatch = useDispatch();

  return (
    <div className="todo-item">
      <span
        className={todo.completed ? "completed" : ""}
        onClick={() => dispatch(toggleTodo(todo.id))}
      >
        {todo.text}
      </span>
      <button onClick={() => dispatch(removeTodo(todo.id))}>❌</button>
    </div>
  );
}

export default TodoItem;
```

---

## 🧠 App.jsx

```jsx
import TodoInput from "./features/todos/TodoInput";
import TodoList from "./features/todos/TodoList";
import "./App.css";

function App() {
  return (
    <div className="app">
      <h1>Redux Toolkit Todo App</h1>
      <TodoInput />
      <TodoList />
    </div>
  );
}

export default App;
```

---

## 🎨 App.css

```css
.app {
  width: 400px;
  margin: 40px auto;
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
}
.todo-input {
  display: flex;
  margin-bottom: 10px;
  gap: 10px;
}
.todo-input input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ddd;
}
.todo-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.completed {
  text-decoration: line-through;
  color: gray;
}
```

---

## 🧠 main.jsx

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { store } from "./app/store";
import { Provider } from "react-redux";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

---

## 📦 What You Learned

🔹 Redux Toolkit setup  
🔹 configureStore  
🔹 createSlice  
🔹 useDispatch  
🔹 useSelector  
🔹 Component-based Redux logic  
🔹 UI styling with CSS

---

## 🧠 Redux Toolkit Patterns

### ✔ Shorter code  
### ✔ No switch statements  
### ✔ Auto-immutability  
### ✔ Better defaults  
### ✔ Recommended by React team

---

## 💡 Interview Tips

### ❓ Why use Redux Toolkit?
👉 Simplifies complicated Redux.

### ❓ Why not use normal Redux?
👉 Too much boilerplate, harder to maintain.

### ❓ When should you use Redux?
👉 Complex global state — many components need the same data.

---

## 🚀 Next Steps

✔ Add async logic with `createAsyncThunk`  
✔ Connect to backend API  
✔ Add filters (completed / active)  
✔ Add persistence (localStorage)

---

## ⭐ Support

If this helped you:

⭐ Star the repo  
🔁 Share with friends  
📘 More React notes coming soon 🎉
