# react-jsx-exercises
Links to codepen exercises.

## 1. Display String
https://codepen.io/bzzz-coding/pen/dyKVvMR

## 2. Display Array of Users
https://codepen.io/bzzz-coding/pen/poKWebM

### Learning Note: 
```
const users = [
  { name: "John Doe", id: 1 },
  { name: "Jane Doe", id: 2 },
  { name: "Billy Doe", id: 3 }
]

{/* inside function App() return: */}
<ul>
  {users.map((user) => (
    <li key={user.id}>{user.name}</li>
  ))}
</ul>
```

