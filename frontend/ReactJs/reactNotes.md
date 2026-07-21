# React.js Crash Course (2026)
> Project Ready Guide for New Team Members

**Target Audience:** Beginners with JavaScript (ES6+) knowledge  
**Duration:** 1-2 Days  
**Goal:** Become ready to work on a production React project.

---

# What is React?

React is a **JavaScript library** for building **fast, interactive, reusable user interfaces (UI)**.

Created by **Meta (Facebook)**.

Instead of manipulating HTML manually, React updates only the changed parts using the **Virtual DOM**.

---

# Why React?

✅ Component-Based Architecture

✅ Reusable Code

✅ Faster UI Updates

✅ Huge Ecosystem

✅ Easy State Management

✅ SEO Support (with Next.js)

✅ Industry Standard

---

# Prerequisites

Before learning React, you should know:

- HTML
- CSS
- JavaScript ES6+
    - let / const
    - Arrow Functions
    - Template Literals
    - Destructuring
    - Spread Operator
    - Rest Parameters
    - Modules
    - Promises
    - Async/Await
    - Array Methods
    - Objects

---

# React Folder Structure

```
src/
│
├── assets/
├── components/
├── pages/
├── layouts/
├── hooks/
├── context/
├── services/
├── utils/
├── constants/
├── styles/
├── App.jsx
└── main.jsx
```

---

# How React Works

```
Browser

↓

main.jsx

↓

<App />

↓

Components

↓

Virtual DOM

↓

Real DOM

↓

UI Updated
```

---

# Create React Project (Vite)

```bash
npm create vite@latest my-app

cd my-app

npm install

npm run dev
```

---

# Project Structure

```
my-app/

node_modules/

public/

src/

App.jsx

main.jsx

package.json

vite.config.js
```

---

# main.jsx

Entry point of React.

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(
    <App />
);
```

---

# App.jsx

Main component.

```jsx
function App() {
    return (
        <h1>Hello React</h1>
    );
}

export default App;
```

---

# JSX

JSX = JavaScript + HTML

Example

```jsx
const name = "John";

return (
    <h1>Hello {name}</h1>
);
```

---

# JSX Rules

Only one parent element

✅

```jsx
return (
    <div>
        <h1></h1>
        <p></p>
    </div>
)
```

OR

```jsx
<>
    ...
</>
```

---

Use

```
className
```

instead of

```
class
```

---

Close every tag

```jsx
<img />
<input />
<br />
```

---

Use JavaScript inside {}

```jsx
<h1>{2 + 2}</h1>
```

---

# Components

A Component is a reusable UI block.

Example

```jsx
function Button() {
    return <button>Click</button>;
}
```

Use

```jsx
<Button />
```

---

# Component Types

Functional Components ✅

Class Components ❌ (Legacy)

---

# Props

Props pass data from Parent → Child.

Parent

```jsx
<User name="Alex" age={25} />
```

Child

```jsx
function User(props) {
    return (
        <>
            <h2>{props.name}</h2>
            <p>{props.age}</p>
        </>
    );
}
```

Destructuring

```jsx
function User({name, age}) {
    ...
}
```

---

# Children Prop

```jsx
<Card>

<h1>Hello</h1>

</Card>
```

```jsx
function Card({children}) {
    return (
        <div>
            {children}
        </div>
    );
}
```

---

# Rendering Lists

```jsx
const users = ["Alex","John","Mike"];

return (

<>
{
users.map(user => (

<p key={user}>{user}</p>

))
}
</>

);
```

Always use

```
key
```

---

# Conditional Rendering

Using &&

```jsx
{isLogin && <Dashboard />}
```

Using Ternary

```jsx
{
isLogin

? <Dashboard/>

: <Login/>
}
```

---

# Event Handling

```jsx
<button onClick={handleClick}>
```

```jsx
function handleClick(){

console.log("Clicked");

}
```

---

# State

State stores changing data.

```jsx
import {useState} from "react";

const [count, setCount] = useState(0);
```

Update

```jsx
setCount(count + 1);
```

Never

```jsx
count = count + 1;
```

---

# Multiple States

```jsx
const [name, setName] = useState("");

const [email, setEmail] = useState("");

const [loading, setLoading] = useState(false);
```

---

# Updating Objects

```jsx
setUser(prev => ({
    ...prev,
    name:"Alex"
}));
```

---

# Updating Arrays

```jsx
setUsers(prev => [...prev,newUser]);
```

---

# Forms

Controlled Components

```jsx
const [name,setName] = useState("");
```

```jsx
<input

value={name}

onChange={(e)=>setName(e.target.value)}

/>
```

---

# useEffect

Runs side effects.

```jsx
useEffect(()=>{

console.log("Loaded");

},[]);
```

---

Run when dependency changes

```jsx
useEffect(()=>{

},[count]);
```

---

Cleanup

```jsx
useEffect(()=>{

const id = setInterval(...);

return ()=>clearInterval(id);

},[]);
```

---

# Fetch API

```jsx
useEffect(()=>{

fetch("/api/users")

.then(res=>res.json())

.then(data=>setUsers(data));

},[]);
```

Modern

```jsx
useEffect(()=>{

async function getUsers(){

const res = await fetch("/api/users");

const data = await res.json();

setUsers(data);

}

getUsers();

},[]);
```

---

# Custom Hooks

```jsx
function useCounter(){

const [count,setCount]=useState(0);

return {count,setCount};

}
```

---

# Context API

Avoids Prop Drilling.

```
App

↓

ThemeProvider

↓

Navbar

↓

Button

↓

Card
```

---

Create Context

```jsx
const ThemeContext = createContext();
```

Provider

```jsx
<ThemeContext.Provider value={{theme}}>

<App/>

</ThemeContext.Provider>
```

Consume

```jsx
const {theme}=useContext(ThemeContext);
```

---

# React Router

Install

```bash
npm i react-router-dom
```

Routes

```jsx
<BrowserRouter>

<Routes>

<Route path="/" element={<Home/>}/>

<Route path="/about" element={<About/>}/>

</Routes>

</BrowserRouter>
```

Navigation

```jsx
<Link to="/about">
```

Programmatic

```jsx
const navigate = useNavigate();

navigate("/dashboard");
```

---

# Common Hooks

| Hook | Purpose |
|--------|----------|
| useState | State |
| useEffect | Side Effects |
| useRef | DOM Reference |
| useMemo | Memoize Values |
| useCallback | Memoize Functions |
| useContext | Global Data |
| useReducer | Complex State |
| useId | Unique IDs |
| useTransition | Non-blocking UI |
| useDeferredValue | Optimize Expensive Rendering |

---

# Component Lifecycle (Functional)

```
Mount

↓

Render

↓

useEffect

↓

Update

↓

Re-render

↓

Cleanup

↓

Unmount
```

---

# Styling Options

- CSS
- CSS Modules
- Tailwind CSS ⭐
- Styled Components
- Emotion

---

# API Handling

Preferred

```
fetch()

axios
```

Always

- Loading State
- Error State
- Empty State

---

# Best Practices

✅ Small Components

✅ Reusable Components

✅ Meaningful Names

✅ Folder Structure

✅ Functional Components

✅ Hooks

✅ Tailwind CSS

✅ Lazy Loading

✅ Error Boundary

✅ Code Splitting

✅ ESLint

✅ Prettier

---

# Common Mistakes

❌ Mutating State

❌ Missing key

❌ Too many Props

❌ Large Components

❌ Unnecessary Re-renders

❌ Missing Cleanup

❌ Inline Anonymous Functions Everywhere

❌ Business Logic Inside JSX

---

# Recommended Packages (2026)

| Purpose | Package |
|----------|----------|
| Routing | react-router-dom |
| HTTP | axios |
| Forms | react-hook-form |
| Validation | zod |
| Icons | lucide-react |
| Animation | framer-motion |
| Notifications | react-toastify |
| State Management | Zustand |
| Data Fetching | TanStack Query |
| Styling | Tailwind CSS |
| Charts | Recharts |

---

# Performance Tips

- Memoize expensive calculations (`useMemo`)
- Memoize callbacks (`useCallback`)
- Use `React.memo`
- Lazy load routes/components
- Virtualize long lists
- Avoid unnecessary state
- Keep components focused

---

# Production Folder Example

```
src/
│
├── api/
├── assets/
├── components/
│   ├── common/
│   ├── ui/
│   └── forms/
│
├── context/
├── features/
├── hooks/
├── layouts/
├── pages/
├── routes/
├── services/
├── store/
├── styles/
├── utils/
├── App.jsx
└── main.jsx
```

---

# Project Workflow

```
Requirement

↓

UI Design

↓

Component Breakdown

↓

Create Layout

↓

Create Components

↓

Manage State

↓

Connect API

↓

Validation

↓

Testing

↓

Optimization

↓

Deployment
```

---

# React Interview Essentials

- What is React?
- Virtual DOM
- JSX
- Components
- Props vs State
- Hooks
- useEffect
- Context API
- Controlled Components
- Keys in Lists
- React.memo
- useMemo vs useCallback
- Reconciliation
- Lifting State Up
- Prop Drilling
- Error Boundaries
- Code Splitting
- Lazy Loading
- React Router
- Performance Optimization

---

# Learning Path After This

1. Advanced React Hooks
2. Custom Hooks
3. Context API
4. Zustand
5. TanStack Query
6. Authentication
7. Protected Routes
8. API Architecture
9. Form Validation
10. React Performance
11. Testing (Vitest + React Testing Library)
12. Next.js App Router
13. Server Components
14. Deployment (Vercel, Netlify)

---

# Final Takeaway

A React developer in **2026** should be comfortable with:

- Component-based architecture
- JSX
- Props & State
- Hooks
- API integration
- Routing
- Forms & Validation
- Context API
- Performance optimization
- Clean project structure
- Tailwind CSS
- Git & GitHub
- Basic testing
- Modern React patterns

Once you master these fundamentals, you'll be ready to contribute effectively to most production React projects.