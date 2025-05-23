# Props, State in react

## State

### What is state

- State is a special object in React used to store a component's internal data.
- When the state changes, React automatically re-renders the component to update the user interface.

### Why need state ?

- HTML/JavaScript does not "remember" data after each change.
- React allows you to remember and update the UI when data changes — thanks to state.

### Example

- The number of times the user clicks a button
- The open/close state of a menu
- The list of products added to the shopping cart

### How to use state

### Function component

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

**\*Explain**

- `useState(0)` Create a state named count with an initial value of 0.
- `setCount` It's the function used to update the value of count.
- When `setCount(...)` is called, React will `re-render` the UI to display the new value.

### Class component

```jsx
import React from "react";

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  handleClick = () => {
    this.setState({
      count: this.state.count + 1,
    });
  };

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={this.handleClick}>Click me</button>
      </div>
    );
  }
}

export default Counter;
```

**\*Explain**

- `constructor` is used to initialize state and calls `super(props)` to inherit from `React.Component`
- `this.state` the internal data of the component
- `this.setState(...)` Updated `state` and auto `re-render` UI
- `render()` returns JSX to render on the interface.

## Props

### What is Props

- Used to pass data from a parent component to a child component.
  -In React, props are the "inputs" of a component that help make the component flexible and reusable.

### Example

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return <Welcome name="William" />;
}
```

**\*Explains**

- `Welcome` is the child component
- name="William" is a prop passed from App to Welcome
- Inside Welcome, we access props.name to use that data
