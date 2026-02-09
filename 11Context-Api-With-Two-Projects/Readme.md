# 🌐 React Context API — Crash Course with 2 Projects

> 📘 Complete Beginner → Intermediate Notes  
> 🎥 Topic: Context API Crash Course  
> 🧠 Focus: Prop drilling, global state, Context, useContext, useReducer  
> 🚀 Includes: 2 mini projects

---

## 📌 What You Will Learn

- What is prop drilling
- Why Context API exists
- How Context works internally
- How to create and use context
- useContext hook
- useReducer with context
- Two mini projects:
  - Theme toggler
  - Global state example

---

## 🤔 The Problem: Prop Drilling

In React, data usually flows like this:

```
App → Parent → Child → GrandChild
```

If **GrandChild** needs data from **App**, we must pass props through every level.

### Example of Prop Drilling

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

### Problems

- Too many props
- Hard to maintain
- Unnecessary components passing data
- Difficult debugging

---

## 🌐 What Is Context API?

Context API allows you to:

✅ Share data globally  
✅ Avoid prop drilling  
✅ Access state anywhere in component tree  

Context is used for:

- Theme
- Auth data
- Language
- Global settings

Context lets components read data **without passing props manually**. :contentReference[oaicite:1]{index=1}

---

## 🧠 Core Idea

Instead of:

```
App → Parent → Child → GrandChild
```

With Context:

```
Context Provider
       ↓
Any Component can access the data
```

---

## 🏗️ Steps to Use Context API

There are **3 main steps**:

1. Create Context
2. Provide Context
3. Consume Context

---

## Step 1: Create Context

```jsx
import { createContext } from "react";

export const ThemeContext = createContext();
```

---

## Step 2: Provide Context

Wrap your app with a Provider.

```jsx
import { ThemeContext } from "./ThemeContext";

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Home />
    </ThemeContext.Provider>
  );
}
```

---

## Step 3: Consume Context (Old Way)

Using **Consumer component**:

```jsx
import { ThemeContext } from "./ThemeContext";

function Home() {
  return (
    <ThemeContext.Consumer>
      {(theme) => <h1>{theme}</h1>}
    </ThemeContext.Consumer>
  );
}
```

---

## Modern Way: useContext Hook

Cleaner and easier.

```jsx
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function Home() {
  const theme = useContext(ThemeContext);

  return <h1>{theme}</h1>;
}
```

---

# 🚀 Project 1: Theme Toggler

Goal:
- Light and dark theme
- Toggle button
- Global theme state

---

## Step 1: Create Context

```jsx
import { createContext } from "react";

export const ThemeContext = createContext();
```

---

## Step 2: Create Provider

```jsx
import { useState } from "react";
import { ThemeContext } from "./ThemeContext";

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  function toggleTheme() {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export default ThemeProvider;
```

---

## Step 3: Wrap App

```jsx
import ThemeProvider from "./ThemeProvider";
import Home from "./Home";

function App() {
  return (
    <ThemeProvider>
      <Home />
    </ThemeProvider>
  );
}
```

---

## Step 4: Use Context in Component

```jsx
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function Home() {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <div
      style={{
        background: theme === "light" ? "#fff" : "#111",
        color: theme === "light" ? "#111" : "#fff",
        height: "100vh",
      }}
    >
      <h1>Current Theme: {theme}</h1>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
}

export default Home;
```

---

# ⚙️ Project 2: Global State with useReducer + Context

Used for:

- Complex state
- Multiple actions
- Global app logic

---

## Step 1: Create Context

```jsx
import { createContext } from "react";

export const CounterContext = createContext();
```

---

## Step 2: Create Reducer

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };

    case "DECREMENT":
      return { count: state.count - 1 };

    default:
      return state;
  }
}
```

---

## Step 3: Create Provider

```jsx
import { useReducer } from "react";
import { CounterContext } from "./CounterContext";

function CounterProvider({ children }) {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <CounterContext.Provider value={{ state, dispatch }}>
      {children}
    </CounterContext.Provider>
  );
}

export default CounterProvider;
```

---

## Step 4: Wrap App

```jsx
import CounterProvider from "./CounterProvider";
import Counter from "./Counter";

function App() {
  return (
    <CounterProvider>
      <Counter />
    </CounterProvider>
  );
}
```

---

## Step 5: Use in Component

```jsx
import { useContext } from "react";
import { CounterContext } from "./CounterContext";

function Counter() {
  const { state, dispatch } = useContext(CounterContext);

  return (
    <div>
      <h1>Count: {state.count}</h1>

      <button onClick={() => dispatch({ type: "INCREMENT" })}>
        +
      </button>

      <button onClick={() => dispatch({ type: "DECREMENT" })}>
        -
      </button>
    </div>
  );
}

export default Counter;
```

---

# 🧠 Key Concepts to Remember

## Context Flow

```
createContext()
      ↓
Provider wraps app
      ↓
useContext() reads data
```

---

## When to Use Context

Use Context for:

- Theme
- Auth
- Language
- Global settings

Avoid for:

- Very frequently changing data
- Huge state logic (use Redux/Zustand instead)

---

## Context vs Props

| Feature | Props | Context |
|--------|------|--------|
| Scope | Parent → Child | Global |
| Setup | Simple | Needs provider |
| Use case | Small data flow | Global state |
| Prop drilling | Yes | No |

---

## Context with useReducer

Best for:

- Complex state
- Multiple actions
- App-level logic

---

# 🧪 Mental Model

Without Context:

```
Data → Passed through every component
```

With Context:

```
Data → Stored globally
Components → Read directly
```

---

# 🧠 Interview Questions

### 1. What is Context API?

Context API is a way to share global data across components without prop drilling. :contentReference[oaicite:2]{index=2}

---

### 2. What problem does Context solve?

It solves **prop drilling**.

---

### 3. What are the main parts of Context?

- createContext
- Provider
- Consumer / useContext

---

### 4. When should you not use Context?

- Very frequent updates
- Large complex state

---

### 5. Difference between Redux and Context?

| Redux | Context |
|------|--------|
| External library | Built into React |
| Complex state | Simple global state |
| Middleware support | No middleware |
| Large apps | Small to medium apps |

---

# 📚 Final Summary

| Concept | Meaning |
|--------|--------|
| Context API | Global state sharing |
| Provider | Supplies data |
| Consumer | Reads data |
| useContext | Hook to access context |
| useReducer | Complex state logic |
| Prop drilling | Passing props through many levels |

---

# ❤️ Final Words

“If props feel painful,  
Context is the relief.”

Context API is:

- Simple
- Built into React
- Powerful for global state

---

⭐ Star the repo  
📘 More React notes coming soon  
🚀 Keep building. Keep committing.
