  <div align="center">

# ⚛️ React Context API — Complete Guide & Projects

### 📘 Practical Explanation + 4 Real Projects  
### 🚀 Beginner Friendly • 🧠 Interview Ready • 💻 Copy-Paste Code

---  
    
</div>

## 📚 Table of Contents

- [What is Context API](#-what-is-context-api)
- [Problem: Prop Drilling](#-the-problem-prop-drilling)
- [Solution: Context API](#-solution-context-api)
- [Core Concepts](#-core-parts-of-context-api)
- [When to Use Context](#-when-to-use-context)
- [Interview Questions](#-interview-questions-context-api)
- [Projects](#-projects)

---

# 🌐 What is Context API?

React **Context API** is a built-in feature that allows you to **share data globally** across components **without passing props through every level**.

> **Context = Global State for React**

---

# 🤯 The Problem: Prop Drilling

Prop drilling happens when data is passed through **multiple components** that don’t actually use it.

### Example

```jsx
function App() {
  return <Parent theme="dark" />;
}

function Parent({ theme }) {
  return <Child theme={theme} />;
}

function Child({ theme }) {
  return <GrandChild theme={theme} />;
}

function GrandChild({ theme }) {
  return <h1>{theme}</h1>;
}
```

### ❌ Problems

- Too many props
- Hard to maintain
- Difficult debugging
- Not scalable

---

# ✅ Solution: Context API

Instead of:

```
App → Parent → Child → GrandChild
```

Context works like:

```
Context Provider
      ↓
Any component can access data directly
```

---

# 🧠 Mental Model

Think of Context like **Wi-Fi** 📡

| Concept | Real World |
|--------|------------|
| Provider | Wi-Fi Router |
| Components | Devices |
| Data | Internet |

If you are inside the Provider → you can access the data.

---

# 🧩 Core Parts of Context API

Context API has **3 main parts**:

1. `createContext()`
2. `Provider`
3. `useContext()`

---

## 1️⃣ createContext()

Creates the global data container.

```jsx
import { createContext } from "react";

export const ThemeContext = createContext();
```

---

## 2️⃣ Provider

Supplies data to the component tree.

```jsx
function ThemeProvider({ children }) {
  const theme = "dark";

  return (
    <ThemeContext.Provider value={theme}>
      {children}
    </ThemeContext.Provider>
  );
}
```

---

## 3️⃣ useContext()

Used to access context data.

```jsx
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function Home() {
  const theme = useContext(ThemeContext);

  return <h1>{theme}</h1>;
}
```

---

# 🔄 How Context Works

1. Context stores a value
2. Provider gives the value
3. Components subscribe using `useContext`
4. When value changes → components re-render

---

# ⚡ Context with State

```jsx
function AppProvider({ children }) {
  const [count, setCount] = useState(0);

  return (
    <AppContext.Provider value={{ count, setCount }}>
      {children}
    </AppContext.Provider>
  );
}
```

---

# ⚙️ Context with useReducer

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "INC":
      return { count: state.count + 1 };
    default:
      return state;
  }
}
```

### Why useReducer?

- Cleaner logic
- Better for complex apps
- Redux-like structure

---

# 🆚 Props vs Context

| Feature | Props | Context |
|--------|------|--------|
| Scope | Parent → Child | Global |
| Prop drilling | Yes | No |
| Setup | Easy | Medium |
| Best for | Small data | Global data |

---

# ❌ When NOT to Use Context

Avoid Context when:

- Data updates very frequently
- Performance is critical
- Very large state (use Redux/Zustand)

---

# ✅ When to Use Context

Perfect for:

- Theme (dark/light)
- Authentication
- Language settings
- Global counters
- Quiz state
- Team data

---

# 🧠 Interview Questions (Context API)

### Q1. What problem does Context solve?
👉 Prop drilling.

### Q2. Is Context a state manager?
👉 No, it only shares state.

### Q3. Context vs Redux?
👉 Context is built-in and simple.  
Redux is external and advanced.

### Q4. Can Context replace Redux?
👉 For small to medium apps, yes.

---

# 🎯 Final Summary

- Context API = Global data sharing
- Removes prop drilling
- Uses Provider + useContext
- Best for app-wide state

> “If props feel painful, Context is the relief.”

---

# 🚀 Projects

---

# 🌓 Project 1: Theme Toggler

### Folder Structure

```
src/
 ├── context/
 │   └── ThemeContext.jsx
 ├── components/
 │   └── ThemeButton.jsx
 ├── App.jsx
 └── main.jsx
```

## ThemeContext.jsx

```jsx
import { createContext, useState } from "react";

export const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [dark, setDark] = useState(false);

  function toggleTheme() {
    setDark(!dark);
  }

  return (
    <ThemeContext.Provider value={{ dark, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

## ThemeButton.jsx

```jsx
import { useContext } from "react";
import { ThemeContext } from "../context/ThemeContext";

function ThemeButton() {
  const { dark, toggleTheme } = useContext(ThemeContext);

  return (
    <div
      style={{
        background: dark ? "#111" : "#fff",
        color: dark ? "#fff" : "#111",
        height: "100vh",
        padding: "40px",
      }}
    >
      <h1>{dark ? "Dark Mode" : "Light Mode"}</h1>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
}

export default ThemeButton;
```

---

# 👤 Project 2: User Auth Context

## AuthContext.jsx

```jsx
import { createContext, useState } from "react";

export const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  function login() {
    setUser("Stavan");
  }

  function logout() {
    setUser(null);
  }

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}
```

---

# ⚽ Project 3: Football Team Lineup Builder

## TeamContext.jsx

```jsx
import { createContext, useState } from "react";

export const TeamContext = createContext();

export function TeamProvider({ children }) {
  const [players, setPlayers] = useState([]);

  function addPlayer(name) {
    setPlayers([...players, name]);
  }

  function removePlayer(name) {
    setPlayers(players.filter((p) => p !== name));
  }

  return (
    <TeamContext.Provider value={{ players, addPlayer, removePlayer }}>
      {children}
    </TeamContext.Provider>
  );
}
```

---

# 🧠 Project 4: Quiz App

## QuizContext.jsx

```jsx
import { createContext, useState } from "react";

export const QuizContext = createContext();

const questions = [
  {
    q: "What is React?",
    a: "Library",
    options: ["Framework", "Library", "Language"],
  },
  {
    q: "JSX stands for?",
    a: "JavaScript XML",
    options: ["JSON", "Java XML", "JavaScript XML"],
  },
];

export function QuizProvider({ children }) {
  const [index, setIndex] = useState(0);
  const [score, setScore] = useState(0);

  function next() {
    setIndex(index + 1);
  }

  return (
    <QuizContext.Provider
      value={{ questions, index, score, setScore, next }}
    >
      {children}
    </QuizContext.Provider>
  );
}
```

---

# 🎯 What You Learn

- Context API fundamentals
- Global state management
- Real-world React patterns
- Component communication
- Interview-ready logic

---

<div align="center">

⭐ Star the repo  
🚀 Keep building  
⚛️ Keep learning React  

</div>
