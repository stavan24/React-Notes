# 🌐 What is React?

**React** is a **JavaScript library** used to build **user interfaces (UI)**, especially for **single-page applications (SPAs)**.  
It helps developers create **dynamic, fast, and reusable components**.

- 🏢 **Created by:** Facebook (Meta)  
<<<<<<< HEAD
- 💻 **Purpose:** Frontend development  
=======
- 💻 **Purpose:** Frontend development   
>>>>>>> 5a824d9823f5e00571841e6496f63ec9e52e9660
- 🧩 **Core Concept:** Component-based architecture

---

## 🔹 Overview

Traditional websites reload the entire page for updates, which can be **slow and inefficient**.  
React updates only the **parts of the UI that change** using a **Virtual DOM**, making apps **faster and smoother** ⚡.

---

## 🔹 Key Features

1. **Component-Based Architecture** 🏗️  
   - Divide UI into **independent, reusable components**  
   - Encourages **modular and maintainable code**

2. **Declarative Syntax** ✏️  
   - Describe **what the UI should look like**  
   - React handles the updates automatically

3. **Efficient Rendering with Virtual DOM** ⚡  
   - Minimizes actual DOM updates  
   - Only re-renders what’s needed

4. **Strong Ecosystem** 🌐  
   - Libraries, tools, and large developer community

---

## 🔹 Example

**React Advantage:**

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
