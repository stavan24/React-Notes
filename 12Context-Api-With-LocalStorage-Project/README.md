# 🗃️ React Context API + Local Storage Project  

> 📘 Context API with localStorage — Full Project  
> 🚀 Real-world React App  
> 🧠 Save tasks persistently + manage global state
         
---                     
                            
## 📌 What You’ll Build          
                          
A **to-do list app** that lets users:        
  
- Add new tasks      
- Mark tasks complete  
- Edit tasks  
- Delete tasks
- Persist tasks in `localStorage`
  
This uses:    
    
✅ React Context API      
✅ `useContext`, `useReducer` / `useState`  
✅ `localStorage` for persistence  
✅ Component-based UI  
✅ CSS styling

---

## 📁 Folder Structure

```
src/
├── context/
│   └── TodoContext.jsx
├── components/
│   ├── TodoInput.jsx
│   ├── TodoList.jsx
│   └── TodoItem.jsx
├── App.jsx
├── App.css
├── main.jsx
└── index.css
```
   
---

## 🧠 Context Setup — TodoContext.jsx

This stores tasks globally and syncs with localStorage.

```jsx
import { createContext, useState, useEffect } from "react";

export const TodoContext = createContext();

export function TodoProvider({ children }) {
  const [todos, setTodos] = useState(
    JSON.parse(localStorage.getItem("todos")) || []
  );

  useEffect(() => {
    localStorage.setItem("todos", JSON.stringify(todos));
  }, [todos]);

  function addTodo(todo) {
    setTodos([...todos, todo]);
  }

  function deleteTodo(id) {
    setTodos(todos.filter((t) => t.id !== id));
  }

  function toggleComplete(id) {
    setTodos(
      todos.map((t) =>
        t.id === id ? { ...t, completed: !t.completed } : t
      )
    );
  }

  return (
    <TodoContext.Provider value={{ todos, addTodo, deleteTodo, toggleComplete }}>
      {children}
    </TodoContext.Provider>
  );
}
```

---

## 🧾 Global CSS — index.css

```css
body {
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  margin: 0;
  padding: 0;
}
```

---

## 🌟 App Component — App.jsx

```jsx
import TodoInput from "./components/TodoInput";
import TodoList from "./components/TodoList";
import "./App.css";

function App() {
  return (
    <div className="app-container">
      <h1>🗒️ Todo App with Context + localStorage</h1>
      <TodoInput />
      <TodoList />
    </div>
  );
}

export default App;
```

---

## 🎨 App Styles — App.css

```css
.app-container {
  width: 400px;
  margin: 50px auto;
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}
```

---

## ✏️ TodoInput.jsx

```jsx
import { useContext, useState } from "react";
import { TodoContext } from "../context/TodoContext";

function TodoInput() {
  const { addTodo } = useContext(TodoContext);
  const [text, setText] = useState("");

  function addTask() {
    if (text.trim() === "") return;

    addTodo({
      id: Date.now(),
      text,
      completed: false,
    });
    setText("");
  }

  return (
    <div className="todo-input">
      <input
        type="text"
        placeholder="Enter task..."
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={addTask}>Add</button>
    </div>
  );
}

export default TodoInput;
```

---

## 📝 TodoInput CSS

Add to `App.css`:

```css
.todo-input {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.todo-input input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
```

---

## 📜 TodoList.jsx

```jsx
import { useContext } from "react";
import { TodoContext } from "../context/TodoContext";
import TodoItem from "./TodoItem";

function TodoList() {
  const { todos } = useContext(TodoContext);

  if (todos.length === 0) return <p>No tasks yet!</p>;

  return (
    <div>
      {todos.map((todo) => (
        <TodoItem key={todo.id} todo={todo} />
      ))}
    </div>
  );
}

export default TodoList;
```

---

## 🧩 TodoItem.jsx

```jsx
import { useContext } from "react";
import { TodoContext } from "../context/TodoContext";

function TodoItem({ todo }) {
  const { deleteTodo, toggleComplete } = useContext(TodoContext);

  return (
    <div className="todo-item">
      <span
        className={todo.completed ? "completed" : ""}
        onClick={() => toggleComplete(todo.id)}
      >
        {todo.text}
      </span>
      <button onClick={() => deleteTodo(todo.id)}>❌</button>
    </div>
  );
}

export default TodoItem;
```

---

## 🧠 TodoItem CSS

Add to `App.css`:

```css
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.todo-item span {
  cursor: pointer;
}

.todo-item span.completed {
  text-decoration: line-through;
  color: gray;
}
```

---

## 🚀 Entry Point — main.jsx

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { TodoProvider } from "./context/TodoContext";

ReactDOM.createRoot(document.getElementById("root")).render(
  <TodoProvider>
    <App />
  </TodoProvider>
);
```

---

## 🧠 How It Works

✔ When app loads, state loads from `localStorage`  
✔ When tasks change, `useEffect` saves them  
✔ Any component can read or update tasks with Context  

This eliminates **prop drilling** and keeps code clean. :contentReference[oaicite:1]{index=1}

---

## 💡 Features You Can Add

- Edit tasks
- Filter by completed/incomplete
- Dark/Light theme  
- Drag & drop reorder

---

## 🧠 Interview Takeaways

- Context API + localStorage is great for **global persistent state**
- `useContext` replaces prop drilling
- `useEffect` keeps localStorage updated  
- Simple but real-world state sharing pattern

---

## ⭐ Final Words

This project is **both educational and practical** — you can use it as a portfolio piece or learning resource.

Happy coding ⚛️🚀





































































