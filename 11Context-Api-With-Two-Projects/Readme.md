# ⚛️ React Context API — 4 Complete Projects

> 📘 Practical Context API Projects 
> 📘 With Explaination
> 🚀 Beginner Friendly  
> 🧠 Copy-paste ready code

---
# 🌐 React Context API — Complete Explanation

> 🧠 Understand Context API from ZERO to REAL PROJECT usage  
> 📘 Written for beginners but useful for interviews  
> 🚀 No confusion, no over-engineering

---

## ❓ What is Context API?

Context API is a **built-in React feature** that allows you to **share data globally** across components **without passing props manually at every level**.

In simple words:

> **Context = Global State for React**

---

## 🤯 The Problem: Prop Drilling

Prop drilling happens when data is passed through **multiple components** that don’t actually need it.

### Example (Prop Drilling)

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

### ❌ Problems with Prop Drilling

- Too many props
- Hard to maintain
- Difficult debugging
- Not scalable for large apps

---

## ✅ Solution: Context API

Context lets you store data **once** and access it **anywhere**.

Instead of:

```
App → Parent → Child → GrandChild
```

Context works like:

```
Context Provider
      ↓
Any component can read data directly
```

---

## 🧠 Mental Model

Think of Context like **Wi-Fi** 📡

- Provider = Router
- Components = Devices
- Data = Internet

If you are inside the Provider, you can access the data.

---

## 🧩 Core Parts of Context API

Context API has **3 main parts**:

1️⃣ `createContext()`  
2️⃣ `Provider`  
3️⃣ `useContext()`  

---

## 1️⃣ createContext()

Used to **create a context object**.

```jsx
import { createContext } from "react";

export const ThemeContext = createContext();
```

This creates a **container** for global data.

---

## 2️⃣ Context Provider

Provider is used to **supply data** to components.

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

👉 Any component inside `ThemeProvider` can access `theme`.

---

## 3️⃣ useContext() Hook

Used to **read data from context**.

```jsx
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function Home() {
  const theme = useContext(ThemeContext);

  return <h1>{theme}</h1>;
}
```

✔ Clean  
✔ Simple  
✔ Modern React way  

---

## 🔄 How Context Works Internally

1. Context stores a value
2. Provider gives the value
3. Components subscribe using `useContext`
4. When value changes → all subscribed components re-render

---

## ⚡ Context with State

Most of the time, Context is used with `useState`.

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

## ⚙️ Context with useReducer

Used for **complex state logic**.

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

Why useReducer?
- Cleaner logic
- Better for large apps
- Redux-like pattern

---

## 🆚 Props vs Context

| Feature | Props | Context |
|------|------|------|
| Scope | Parent → Child | Global |
| Prop drilling | Yes | No |
| Setup | Easy | Medium |
| Best for | Small data | Global data |

---

## ❌ When NOT to Use Context

Avoid Context when:

- Data changes very frequently
- Performance is critical
- Huge complex state (use Redux/Zustand)

---

## ✅ When to Use Context

Perfect for:

- Theme (dark/light)
- Authentication (user login)
- Language selection
- App settings
- Global counters
- Quiz state
- Team builder data

---

## 🧠 Interview Questions (Context API)

### Q1. What problem does Context API solve?
👉 Prop drilling.

### Q2. Is Context a state manager?
👉 No, it only shares state.

### Q3. Difference between Redux and Context?
👉 Redux is external + advanced, Context is built-in + simple.

### Q4. Can Context replace Redux?
👉 For small/medium apps, YES.

---

## 🎯 Final Summary

- Context API = Global data sharing
- Eliminates prop drilling
- Uses Provider + useContext
- Best for app-wide state
- Clean and powerful when used correctly

---

## ❤️ Final Words

> “If props feel painful, Context is the relief.”

Once you master Context API,
👉 Redux becomes easier  
👉 Large apps feel simpler  
👉 React makes more sense  


---

# PROJECT 1: THEME TOGGLER (LIGHT/DARK MODE)

---

## Folder Structure

```
src/
 ├── context/
 │   └── ThemeContext.jsx
 ├── components/
 │   └── ThemeButton.jsx
 ├── App.jsx
 └── main.jsx
```

---

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

---

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
      <button onClick={toggleTheme}>
        Toggle Theme
      </button>
    </div>
  );
}

export default ThemeButton;
```

---

## App.jsx

```jsx
import ThemeButton from "./components/ThemeButton";

function App() {
  return <ThemeButton />;
}

export default App;
```

---

## main.jsx

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { ThemeProvider } from "./context/ThemeContext";

ReactDOM.createRoot(document.getElementById("root")).render(
  <ThemeProvider>
    <App />
  </ThemeProvider>
);
```

---

# PROJECT 2: USER AUTH CONTEXT

---

## Folder Structure

```
src/
 ├── context/
 │   └── AuthContext.jsx
 ├── components/
 │   └── Profile.jsx
 ├── App.jsx
 └── main.jsx
```

---

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

## Profile.jsx

```jsx
import { useContext } from "react";
import { AuthContext } from "../context/AuthContext";

function Profile() {
  const { user, login, logout } = useContext(AuthContext);

  return (
    <div>
      <h1>User Profile</h1>
      {user ? (
        <>
          <h2>Welcome, {user}</h2>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <button onClick={login}>Login</button>
      )}
    </div>
  );
}

export default Profile;
```

---

## App.jsx

```jsx
import Profile from "./components/Profile";

function App() {
  return <Profile />;
}

export default App;
```

---

## main.jsx

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { AuthProvider } from "./context/AuthContext";

ReactDOM.createRoot(document.getElementById("root")).render(
  <AuthProvider>
    <App />
  </AuthProvider>
);
```

---

# PROJECT 3: FOOTBALL TEAM LINEUP BUILDER

---

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

## PlayerList.jsx

```jsx
import { useContext, useState } from "react";
import { TeamContext } from "../context/TeamContext";

function PlayerList() {
  const { addPlayer } = useContext(TeamContext);
  const [name, setName] = useState("");

  return (
    <div>
      <h2>Add Player</h2>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Player name"
      />
      <button onClick={() => addPlayer(name)}>Add</button>
    </div>
  );
}

export default PlayerList;
```

---

## Lineup.jsx

```jsx
import { useContext } from "react";
import { TeamContext } from "../context/TeamContext";

function Lineup() {
  const { players, removePlayer } = useContext(TeamContext);

  return (
    <div>
      <h2>Team Lineup</h2>
      {players.map((p) => (
        <div key={p}>
          {p}
          <button onClick={() => removePlayer(p)}>❌</button>
        </div>
      ))}
    </div>
  );
}

export default Lineup;
```

---

## App.jsx

```jsx
import PlayerList from "./components/PlayerList";
import Lineup from "./components/Lineup";

function App() {
  return (
    <div>
      <h1>⚽ Team Builder</h1>
      <PlayerList />
      <Lineup />
    </div>
  );
}

export default App;
```

---

# PROJECT 4: QUIZ APP

---

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

## Question.jsx

```jsx
import { useContext } from "react";
import { QuizContext } from "../context/QuizContext";

function Question() {
  const { questions, index, setScore, next } = useContext(QuizContext);
  const current = questions[index];

  if (!current) return null;

  function check(ans) {
    if (ans === current.a) setScore((s) => s + 1);
    next();
  }

  return (
    <div>
      <h2>{current.q}</h2>
      {current.options.map((opt) => (
        <button key={opt} onClick={() => check(opt)}>
          {opt}
        </button>
      ))}
    </div>
  );
}

export default Question;
```

---

## Result.jsx

```jsx
import { useContext } from "react";
import { QuizContext } from "../context/QuizContext";

function Result() {
  const { score, questions, index } = useContext(QuizContext);

  if (index < questions.length) return null;

  return <h2>Final Score: {score}/{questions.length}</h2>;
}

export default Result;
```

---

## App.jsx

```jsx
import Question from "./components/Question";
import Result from "./components/Result";

function App() {
  return (
    <div>   
      <h1>Quiz App</h1>
      <Question />
      <Result />
    </div>
  );
}

export default App;
```

---

# 🎯 What You Learn

- Context API fundamentals
- Global state management
- Real-world React patterns
- Component communication
- Interview-ready logic

---

⭐ Star the repo  
🚀 Keep building  
⚛️ Keep learning React
