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

## 4. 2-way Data Binding
https://codepen.io/bzzz-coding/pen/JjZrWqM

### Learning Note:
- Have each attribute on separate line; 
- Set value to {text}; 
- Don't forget to pass in e in onChange for input

```
function App() {
  const [text, setText] = React.useState("");

  return (
    <>
      <input
        onChange={(e) => setText(e.target.value)}
        value={text}
        type="text"
        placeholder="Enter Text"
      />
      <p>{text}</p>
    </>
  );
}
```

## 5. Disable Button If Input Is Empty
https://codepen.io/bzzz-coding/pen/gOKGGaJ

### Learning Note:
At first, I was trying to "hide" the entire button with 
`{text.length > 0 && <button>Submit</button>}`

However, this is not "disable" means. Instead, I should use the disabled attribute. The disabled attribute also prevents the onClick event from firing.

```
function App() {
  const [value, setValue] = React.useState("");

  return (
    <>
      <h3>Disable Button Challenge</h3>
      <input type="text" onChange={(e) => setValue(e.target.value)} />
      <button disabled={value.length < 1}>Submit</button>
    </>
  );
}
```

The code below (although not part of this exercise), shows how to disable a button once it has been clicked.
```
function App() {
  const [value, setValue] = React.useState("");
  const [clicked, setClicked] = React.useState(false)

  return (
    <>
      <h3>Disable Button After It Has Been Clicked Once</h3>
      <button onClick={() => setClicked(true)} disabled={clicked}>{clicked ? 'You have clicked this button' : 'You can click this button once'}</button>
    </>
  );
}
```

## 6. Update Parent State From Child
https://codepen.io/bzzz-coding/pen/xxzXXeM

### My solution was to create a function called updateText, and passed it down using prop updateParentText to the child:
```
function Child({updateParentText}) {
 
  return (
    <>
      <div>Child</div>
      <button onClick={updateParentText}>Change Parent Value</button>
    </>
  );
}

function Parent() {
  const [value, setValue] = React.useState(
    "I need to be updated from my child"
  );
  
  const updateText = () => {
    setValue('Text updated!')
  }

  return (
    <>
      <h3>Update Parent State Challenge (Using Callback)</h3>
      <div className="wrapper">
        <div>Parent</div>
        <div className="box-wrapper">{value}</div>
      </div>

      <div className="wrapper">
        <Child updateParentText={updateText} />
      </div>
    </>
  );
}

ReactDOM.render(<Parent />, document.getElementById("root"));
```
### Learning Note:
The solution code passed down setValue instead of updateParentText. I'm not sure which is better, but the code looks simpler this way:
```
function Child({ setValue }) {
  return (
    <>
      <div>Child</div>
      <button onClick={() => setValue("Parent has been updated!")}>
        Change Parent Value
      </button>
    </>
  );
}

function Parent() {
  const [value, setValue] = React.useState(
    "I need to be updated from my child"
  );

  return (
    <>
      <h3>Update Parent State Challenge (Using Callback)</h3>
      <div className="wrapper">
        <div>Parent</div>
        <div className="box-wrapper">{value}</div>
      </div>

      <div className="wrapper">
        <Child setValue={setValue} />
      </div>
    </>
  );
}
```

## 7. Dynamically add child components
https://codepen.io/bzzz-coding/pen/dyKVmzY

### Learning Note:
- props.children
Whenever the Parent component is invoked {children} will be displayed. This is a reference to what is between the opening and closing tags of the Parent component.

```
function Child() {
  return <div>This is children content</div>;
}

// Add code only here
function Parent({children}) {
  return (
    <div>
      <h3>Parent Component</h3>
      {children}
    </div>
  );
}

function App() {
  return (
    <Parent>
      <Child />
    </Parent>
  );
}
```

## 8. Adding Two Number Inputs And Displaying Total
My Solution: https://codepen.io/bzzz-coding/pen/QWxOWVr
Solution: https://codepen.io/angelo_jin/pen/BawrWzy

### Learning Note:
- Even when setting input type to "number", the `e.target.value` onChange has a type of String. My solution was to convert the two number strings into numbers in the addNums function. However, I could also do the conversion in the input onChange:
```
onChange={(e) => setNumber1(+e.target.value)}
```

- Total was set to 0 in useState, so the paragraph would show "Total: 0" if I add {total} to the <p> tag: `<p>Total: {total}</p>`. The solution used `<p>Total: {total || ""}</p>` to avoid displaying 0 before calculation.
