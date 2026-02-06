# ⚛️ React Router DOM — Crash Course Notes

> 📘 Complete React Router Notes (Beginner → Interview Ready)  
> 🎥 Based on: *React Router Crash Course*  
> 🎯 Covers routing, navigation, params, nested routes & more

---

## 🚀 Why React Router Is Important

React by default is a **Single Page Application (SPA)**.

That means:
- Only **one HTML page**
- No page reloads
- UI changes using JavaScript

👉 React Router helps us create **multiple pages experience** inside a SPA.

---

## 🧠 What Is React Router?

**React Router** is a library used for:
- Page navigation
- URL-based rendering
- Dynamic routes
- Nested routes

It keeps UI and URL **in sync**.

---

## 📦 Installing React Router

```bash
npm install react-router-dom
📁 Basic Folder Structure
src/
│
├── components/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Contact.jsx
│
├── App.jsx
└── main.jsx
```
🌐 BrowserRouter Setup
📄 main.jsx
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
📌 BrowserRouter wraps the entire app and enables routing.

🧭 Routes & Route
📄 App.jsx
import { Routes, Route } from "react-router-dom";
import Home from "./components/Home";
import About from "./components/About";
import Contact from "./components/Contact";

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="/contact" element={<Contact />} />
    </Routes>
  );
}

export default App;
```
🧩 Creating Pages
📄 Home.jsx
```jsx
function Home() {
  return <h1>Home Page</h1>;
}

export default Home;
```
📄 About.jsx
```jsx
function About() {
  return <h1>About Page</h1>;
}

export default About;
```
🔗 Navigation Using Link
❌ NEVER use `<a>` tags in React Router
✅ Use Link
```jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  );
}

export default Navbar;
```
📌 Prevents page reload.

🧠 NavLink (Active Styling)
```jsx
import { NavLink } from "react-router-dom";

<NavLink
  to="/about"
  className={({ isActive }) => (isActive ? "active" : "")}
>
  About
</NavLink>
```
📌 Automatically adds active state.

🔀 Dynamic Routes (URL Params)
📄 Route Setup
```jsx
<Route path="/user/:id" element={<User />} />
📄 User.jsx
import { useParams } from "react-router-dom";

function User() {
  const { id } = useParams();

  return <h1>User ID: {id}</h1>;
}

export default User;
```
🧠 Why Dynamic Routes?
Used for:

User profiles

Product pages

Blog posts

Example:
```
/user/101
/product/iphone
```
🧭 Programmatic Navigation — useNavigate
```
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  function handleLogin() {
    navigate("/dashboard");
  }

  return <button onClick={handleLogin}>Login</button>;
}
```
🧩 Nested Routes
📄 Parent Route
```
<Route path="/dashboard" element={<Dashboard />}>
  <Route path="profile" element={<Profile />} />
  <Route path="settings" element={<Settings />} />
</Route>
📄 Dashboard.jsx
import { Outlet } from "react-router-dom";

function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>
      <Outlet />
    </div>
  );
}

export default Dashboard;
```
❌ 404 Page (Not Found)
```
<Route path="*" element={<NotFound />} />
function NotFound() {
  return <h1>404 Page Not Found</h1>;
}
```
🧠 Important Interview Concepts
React Router works on client side

No full page reload

Uses history API
```
<Routes> replaces <Switch>
```
Link replaces `<a>`
```
📊 React Router Cheat Sheet
Feature	Hook / Component
Navigation	Link, NavLink
Routing	Routes, Route
Params	useParams
Redirect	useNavigate
Nested Routes	Outlet
❌ Common Mistakes
❌ Using `<a href="">`
❌ Forgetting BrowserRouter
❌ Wrong path nesting
❌ Not using Outlet
```
```
🧠 Mental Model
URL changes
   ↓
React Router matches route
   ↓
Component renders
⭐ Final Words
React Router is mandatory for real React apps.
```
If you understand:

Routing

Params

Navigation

Nested routes

👉 You’re production-ready 🚀

⭐ Support
If these notes helped you:
```
⭐ Star the repo
🔁 Share with friends
📘 More React notes coming soon
```
```
🔥 Happy Routing
⚛️ Keep Building
🚀 Keep Shipping
```
