# ⚛️ React Props & Tailwind CSS

> 📘 Beginner-Friendly Notes  
> 🎥 Topic: Using Props & Tailwind in React  
> ⭐ Covers how to pass data in React and style with Tailwind CSS

---

## 💡 What This Video Teaches

This lesson shows:

- How **props** work in React  
- How to use **Tailwind CSS** for styling  
- Passing data between components  
- Dynamic rendering in React

*(Note: video title indicates “Tailwind and Props in reactjs”) :contentReference[oaicite:1]{index=1}*

---

## 🧠 What Are Props in React?

**Props** (short for *properties*) are how we send data **from one component to another** in React.

React components are like functions:

```jsx
function Greeting(props) {
  return <h1>Hello {props.name}</h1>;
}
```
Here:

Greeting is a component

props.name is data passed into it

🔁 Example: Passing Props
Parent Component
```jsx
function App() {
  return <Greeting name="Stavan" />;
}
```
Child Component
```jsx
function Greeting(props) {
  return <h1>Hello {props.name}!</h1>;
}
```
Output:
```
Hello Stavan!
Props let you reuse components with different data.
```
💬 Props Are Read-Only
Props are immutable:

❌ You cannot change them inside the child component.

Right:
```jsx
<Greeting name="Vaibhav" />
```
Wrong:

props.name = "No"; // ❌ don’t do this
Props should be treated as constant inputs.

🏗 Props For Rendering Lists
React can use props to render dynamic lists:
```jsx
function PostList({ posts }) {
  return (
    <div>
      {posts.map((post, i) => (
        <Post title={post.title} key={i} />
      ))}
    </div>
  );
}
```
Here:

posts is an array passed as prop

.map() renders each item

🐣 Default Props Pattern
A component can provide default values:
```jsx
function UserCard({ name = "Guest" }) {
  return <h2>{name}</h2>;
}
```
This way, the component still works even if no prop is passed.

🎨 Tailwind CSS in React
Tailwind CSS lets you style React components using utility classes.

Example
Instead of writing CSS rules:
```css
.title {
  font-size: 2rem;
  font-weight: bold;
}
```
With Tailwind:
```html
<h1 className="text-2xl font-bold text-center text-blue-500">
  Hello World
</h1>
```
Tailwind classes are:

Utility-first

Very descriptive

Easy to compose

⚛️ Combining React Props with Tailwind
Props can control styles too!
```jsx
function Button({ label, type }) {
  return (
    <button className={`px-4 py-2 rounded ${type}`}>
      {label}
    </button>
  );
}
```
Then when using:


Tailwind styles adjust component appearance dynamically.

📌 Good Practices With Props
✔ Name props clearly
✔ Keep props simple
✔ Use default props
✔ Break UI into small components
✔ Pass only needed data

🧠 Why Props Matter
Props:

Make components reusable

Keep UI logic clean

Help separate data from UI

Enable composition of UI blocks

🧪 Example: App With Props & Tailwind
```jsx
function ProfileCard({ name, role }) {
  return (
    <div className="p-4 shadow rounded border border-gray-200">
      <h2 className="text-xl font-semibold">{name}</h2>
      <p className="text-sm text-gray-600">{role}</p>
    </div>
  );
}
```
```jsx
function App() {
  return (
    <div className="flex gap-4">
      <ProfileCard name="Stavan" role="Developer" />
      <ProfileCard name="Vaibhav" role="Designer" />
    </div>
  );
}

export default App;
```
```
📚 Final Summary
Topic	What You Learn
Props	Passing data between components
Tailwind CSS	Utility classes for styling
Dynamic UI	JSX + props renders different UI
Reusable Components	Breaking UI into pieces
❤️ Final Words
React props + Tailwind CSS =
Clean UI + Reusable logic + Stylish components.
```
⭐ Support
If this helped you:
```
⭐ Star the repository
🔁 Share with friends
📘 More React notes coming soon
```
🔥 Keep learning React + Tailwind! ⚛️
