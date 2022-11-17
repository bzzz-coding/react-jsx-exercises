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

## 3. Show/Hide An Element
https://codepen.io/bzzz-coding/pen/JjZrWyN

### Learning Note:
In the beginning, I was trying to toggle .hidden in the className of the div, and added disply: none; to .hidden in css. Then, I realized that I can just use a ternary operator on the entire div element. This way, there is no need for className or css.

Tip: ternary operators can be used for className, text content, or an entire element.

```
function App() {
  const [showMsg, setShowMsg] = React.useState(true);

  const toggle = () => {
    setShowMsg(!showMsg);
  };

  return (
    <>
      <button onClick={toggle}>
        {showMsg ? "Hide Element Below" : "Show Element Below"}
      </button>

      {showMsg && <div>Toggle Challenge</div>}
    </>
  );
}
```
