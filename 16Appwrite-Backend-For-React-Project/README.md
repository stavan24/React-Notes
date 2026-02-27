# ⚛️ React + Appwrite Backend — Complete Notes

> 📘 Based on Appwrite Backend for React  
> 🚀 Build Full Stack Apps Without Firebase  
> 🧠 Auth + Database + Storage  
> ⭐ Beginner → Production Ready Guide

---

# 🌐 What is Appwrite?

Appwrite is an **open-source Backend-as-a-Service (BaaS)** that provides:

✅ Authentication  
✅ Database  
✅ Storage  
✅ API  
✅ Security  
✅ Realtime updates  

👉 It replaces building your own backend.

Think:

React = Frontend  
Appwrite = Backend  

---

# 🤯 Why Use Appwrite?
```
Without backend:
❌ No login system  
❌ No user data  
❌ No database  
❌ No file upload  
```
```
With Appwrite:
✅ Full backend in minutes  
✅ Secure authentication  
✅ Easy API usage  
✅ Production-ready apps  
```
---

# 🧱 App Architecture
```

React App
↓
Appwrite SDK
↓
Appwrite Server
↓
Database / Auth / Storage

```
---

# 🚀 Step 1 — Create Appwrite Project

1. Install Appwrite locally OR use cloud
2. Create new project
3. Copy Project ID
4. Create database
5. Create collection
6. Enable authentication

---

# 📦 Install Appwrite in React

```jsx
npm install appwrite
```
# 📁 Recommended Folder Structure
```
src/
 ├── appwrite/
 │   ├── config.js
 │   ├── auth.js
 │   └── database.js
 ├── components/
 │   ├── Login.jsx
 │   ├── Signup.jsx
 │   └── Dashboard.jsx
 ├── App.jsx
 └── main.jsx
 ```
⚙️ Appwrite Configuration
appwrite/config.js
```
import { Client } from "appwrite";

const client = new Client();

client
  .setEndpoint("https://cloud.appwrite.io/v1")
  .setProject("YOUR_PROJECT_ID");

export default client;
```
🔐 Authentication Service
appwrite/auth.js
```
import { Account } from "appwrite";
import client from "./config";

const account = new Account(client);

export const signup = (email, password) => {
  return account.create("unique()", email, password);
};

export const login = (email, password) => {
  return account.createEmailPasswordSession(email, password);
};

export const logout = () => {
  return account.deleteSession("current");
};

export const getCurrentUser = () => {
  return account.get();
};
🗄 Database Service
appwrite/database.js
import { Databases } from "appwrite";
import client from "./config";

const databases = new Databases(client);

export const addDocument = (data) => {
  return databases.createDocument(
    "DATABASE_ID",
    "COLLECTION_ID",
    "unique()",
    data
  );
};

export const getDocuments = () => {
  return databases.listDocuments("DATABASE_ID", "COLLECTION_ID");
};
🧩 Signup Component
import { useState } from "react";
import { signup } from "../appwrite/auth";

function Signup() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  async function handleSignup() {
    try {
      await signup(email, password);
      alert("Account created!");
    } catch (err) {
      console.error(err);
    }
  }

  return (
    <div>
      <h2>Signup</h2>
      <input onChange={(e) => setEmail(e.target.value)} placeholder="Email" />
      <input onChange={(e) => setPassword(e.target.value)} placeholder="Password" />
      <button onClick={handleSignup}>Signup</button>
    </div>
  );
}

export default Signup;
```
🔐 Login Component
```
import { useState } from "react";
import { login } from "../appwrite/auth";

function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  async function handleLogin() {
    try {
      await login(email, password);
      alert("Logged in!");
    } catch (err) {
      console.error(err);
    }
  }

  return (
    <div>
      <h2>Login</h2>
      <input onChange={(e) => setEmail(e.target.value)} />
      <input onChange={(e) => setPassword(e.target.value)} />
      <button onClick={handleLogin}>Login</button>
    </div>
  );
}

export default Login;
```
📊 Dashboard With Database
```
import { useEffect, useState } from "react";
import { addDocument, getDocuments } from "../appwrite/database";

function Dashboard() {
  const [docs, setDocs] = useState([]);

  async function loadData() {
    const res = await getDocuments();
    setDocs(res.documents);
  }

  async function addData() {
    await addDocument({ text: "Hello Appwrite" });
    loadData();
  }

  useEffect(() => {
    loadData();
  }, []);

  return (
    <div>
      <h2>Dashboard</h2>
      <button onClick={addData}>Add Data</button>

      {docs.map((doc) => (
        <p key={doc.$id}>{doc.text}</p>
      ))}
    </div>
  );
}

export default Dashboard;
```
🧠 App.jsx
```
import Signup from "./components/Signup";
import Login from "./components/Login";
import Dashboard from "./components/Dashboard";

function App() {
  return (
    <div>
      <h1>React + Appwrite App</h1>
      <Signup />
      <Login />
      <Dashboard />
    </div>
  );
}

export default App;
```
# 🎯 What You Learn
```

✅ Real backend integration
✅ Authentication system
✅ Database CRUD
✅ API communication
✅ Production-ready architecture
```
# 🧠 Interview Questions
```

Q. What is Appwrite?
👉 Open-source Backend-as-a-Service.

Q. Why use Appwrite instead of Firebase?
👉 Open-source + self-hostable + privacy control.

Q. What services does Appwrite provide?
👉 Auth, Database, Storage, Functions.
```
⭐ Final Words

Frontend alone is not enough.
Real developers build full-stack apps.

With React + Appwrite you can build:
```
✅ Social apps
✅ Portfolio with login
✅ Notes app with database
✅ Football team manager ⚽
```
```
⭐ Star the repo
🚀 Build real apps
⚛️ Become production-ready
```
