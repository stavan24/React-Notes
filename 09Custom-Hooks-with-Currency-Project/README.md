# ⚛️ React Custom Hooks — Currency Converter Project (Deep Notes)

> 📘 Advanced React Notes (Beginner → Pro)  
> 🎥 Based on: *Custom Hooks in React | Currency Converter Project*  
> 🎯 Focus: Custom Hooks, API calls, clean architecture, reusability

---

## 🚀 Why This Topic Is Important

Custom Hooks are a **game-changer** in React.

If you understand:
- how to **create custom hooks**
- how to **reuse logic**
- how to **separate UI & logic**

👉 Your React code instantly becomes **cleaner, scalable, and professional**.

This topic is also **VERY IMPORTANT for interviews**.

---

## 🧠 What Are Custom Hooks?

A **Custom Hook** is:

- Just a **JavaScript function**
- Name must start with `use`
- Uses React hooks inside (`useState`, `useEffect`, etc.)
- Returns reusable logic

⚠️ Custom hooks do NOT return JSX  
⚠️ They return **data or functions**

---

## 🪝 Why We Need Custom Hooks

Without custom hooks ❌:
- Repeated logic
- Messy components
- Hard to maintain code

With custom hooks ✅:
- Reusable logic
- Clean UI components
- Better architecture

---

## 📁 Project Folder Structure

```
src/
│
├── hooks/
│   └── useCurrencyInfo.js
│
├── components/
│   └── InputBox.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```
🧠 The Problem We Are Solving
We want to:

Fetch currency rates

Convert one currency to another

Keep UI clean

Reuse logic

👉 Perfect use-case for Custom Hook

🪝 Creating a Custom Hook — useCurrencyInfo
📄 useCurrencyInfo.js
```jsx
import { useEffect, useState } from "react";

function useCurrencyInfo(currency) {
  const [data, setData] = useState({});

  useEffect(() => {
    fetch(
      `https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/${currency}.json`
    )
      .then((res) => res.json())
      .then((res) => setData(res[currency]));
  }, [currency]);

  return data;
}

export default useCurrencyInfo;
```
🔍 What’s Happening Here?
currency is passed as argument

API is called when currency changes

Data is stored in state

Hook returns currency rates

📌 This hook can now be reused ANYWHERE

🧩 Input Component — Clean UI
📄 InputBox.jsx
```jsx
function InputBox({
  label,
  amount,
  onAmountChange,
  currencyOptions = [],
  selectCurrency,
  onCurrencyChange,
}) {
  return (
    <div className="input-box">
      <label>{label}</label>

      <input
        type="number"
        value={amount}
        onChange={(e) =>
          onAmountChange && onAmountChange(Number(e.target.value))
        }
      />

      <select
        value={selectCurrency}
        onChange={(e) =>
          onCurrencyChange && onCurrencyChange(e.target.value)
        }
      >
        {currencyOptions.map((currency) => (
          <option key={currency} value={currency}>
            {currency.toUpperCase()}
          </option>
        ))}
      </select>
    </div>
  );
}

export default InputBox;
```
🧠 Why This Component Is Good
✔ Reusable
✔ Controlled inputs
✔ No business logic
✔ Pure UI component

⚛️ Main App Logic
📄 App.jsx
```jsx
import { useState } from "react";
import InputBox from "./components/InputBox";
import useCurrencyInfo from "./hooks/useCurrencyInfo";

function App() {
  const [amount, setAmount] = useState(1);
  const [from, setFrom] = useState("usd");
  const [to, setTo] = useState("inr");
  const [convertedAmount, setConvertedAmount] = useState(0);

  const currencyInfo = useCurrencyInfo(from);
  const options = Object.keys(currencyInfo);

  const convert = () => {
    setConvertedAmount(amount * currencyInfo[to]);
  };

  const swap = () => {
    setFrom(to);
    setTo(from);
    setConvertedAmount(amount);
    setAmount(convertedAmount);
  };

  return (
    <div className="app">
      <h1>Currency Converter</h1>

      <InputBox
        label="From"
        amount={amount}
        onAmountChange={setAmount}
        currencyOptions={options}
        selectCurrency={from}
        onCurrencyChange={setFrom}
      />

      <button onClick={swap}>Swap</button>

      <InputBox
        label="To"
        amount={convertedAmount}
        currencyOptions={options}
        selectCurrency={to}
        onCurrencyChange={setTo}
      />

      <button onClick={convert}>Convert</button>
    </div>
  );
}

export default App;
```
```
🔄 Data Flow Explained
User changes currency
      ↓
useCurrencyInfo runs
      ↓
API fetch happens
      ↓
Rates stored in hook state
      ↓
App uses updated data
      ↓
UI updates
🧠 Key React Concepts Used
Concept	Usage
useState	Manage amount & currency
useEffect	API call
Custom Hook	Reusable logic
Controlled Inputs	Form handling
Props	Component communication
🧠 Interview Questions From This Topic
❓ What is a custom hook?
A reusable function that uses React hooks and shares logic.

❓ Why name must start with use?
So React can enforce hook rules.

❓ Can hooks return JSX?
❌ No. Only data/functions.

❓ When should you create custom hooks?
When logic repeats across components.
```
❌ Common Mistakes
```
if (condition) {
  useEffect(() => {});
}
```
❌ Hooks cannot be conditional

✅ Correct Pattern
```
useEffect(() => {
  if (condition) {
    // logic
  }
}, [condition]);
```
🧠 Mental Model (IMPORTANT)
Component = UI
Custom Hook = Logic
Keep them separate.

⭐ Final Summary
Custom hooks make React powerful

They help reuse logic

Keep components clean

Improve scalability

Interview favorite topic

If you master custom hooks →
You are no longer a beginner. 🔥

⭐ Support
If these notes helped you:
```
⭐ Star the repo
🔁 Share with friends
📘 More React internals coming soon
```
```
🔥 Happy Coding
⚛️ Keep Building
🚀 Keep Shipping
```
