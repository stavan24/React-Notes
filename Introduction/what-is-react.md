# What is React?

**React** is a **JavaScript library** for building **user interfaces**, primarily for **single-page applications (SPAs)**.  
It enables developers to create **dynamic, fast, and reusable UI components**.

- **Created by:** Facebook (Meta)  
- **Purpose:** Frontend development  
- **Core Concept:** Component-based architecture

---

## Overview

Traditional web applications reload the entire page for updates, which can be slow and inefficient.  
React, on the other hand, updates only the parts of the UI that change, using a **Virtual DOM**, resulting in **faster performance** and **better user experience**.

---

## Key Features

1. **Component-Based Architecture**  
   - UI is divided into **independent, reusable components**.  
   - Encourages modular and maintainable code.

2. **Declarative Syntax**  
   - Developers describe **what the UI should look like**, and React handles updates efficiently.

3. **Efficient Rendering with Virtual DOM**  
   - Minimizes actual DOM manipulation  
   - Updates only the necessary elements

4. **Strong Ecosystem**  
   - Rich libraries, tools, and a large developer community

---

## Example

**Traditional approach (manual DOM updates):**

```javascript
document.getElementById("count").innerText = 1;
