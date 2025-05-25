# Introduce React & JSX

## What is ReactJS ?

- ReactJS is a JavaScript library for building user interfaces, especially Single Page Applications (SPAs). It was developed by Facebook and is maintained by Meta and a community of developers.

## What is Single Page Application ?

- A Single Page Application (SPA) is a web application or website that loads a single HTML page and dynamically updates the content as the user interacts with the app — without requiring a full page reload

### Key Features

- Loads a single HTML page initially
- Dynamically updates the content on the page without refreshing the entire page

## What is Virtual DOM ?

- Virtual DOM is a lightweight copy stored in memory of the real DOM tree (Document Object Model) in the browser. It helps React manage and update the UI more efficiently.
- React uses the Virtual DOM to optimize UI updates.
- When changes occur, React compares the Virtual DOM with the real DOM and updates only the necessary parts.

## Advantage of R of React ?

- High performance thanks to the Virtual DOM
- Reusable components
- Large community and extensive library support
- Strong support for developing Single Page Applications (SPAs)
- Easy to learn and integrate

## Disadvantage of React ?

- Rapidly evolving ecosystem
- Requires a lot of boilerplate code
- Challenging for SEO
- Not a fully-featured framework
- Debugging can be more complex
- Bundle size can grow quickly

## What is JSX?

- JSX (JavaScript XML) is an extension syntax for JavaScript that allows you to write code with a structure similar to HTML inside JavaScript. It helps you describe the user interface (UI) more intuitively when working with React.

```jsx
const element = <h1>Hello, world!</h1>;
```

## Component in React

### Function Component

- It is a simple JavaScript function that returns JSX to describe the UI.
- The syntax is concise and easy to understand, and it is widely used today.
- You can use React Hooks (such as useState, useEffect, useCallback, useMemo) to manage state and side effects.

```jsx
function Header() {
  return <h1>Welcome to React</h1>;
}
```

### Class Component

- It is a class that extends from React.Component.
- It has a render() method that returns JSX.
- State is managed using this.state and updated with this.setState().
- It includes lifecycle methods (e.g., componentDidMount, componentDidUpdate, componentWillUnmount) to handle tasks during the component's lifecycle.

```jsx
import React from "react";

class Header extends React.Component {
  render() {
    return <h1>Welcome to React (Class Component)</h1>;
  }
}
```

## Styling

### Inline styles in JSX

- Using `style` attribute
- CamelCase for properties

```jsx
import React from "react";
function MyComponent() {
  const styles = {
    color: "red",
    fontSize: "16px",
    fontWeight: "bold",
    backgroundColor: "lightblue",
    padding: "10px",
    borderRadius: "5px",
  };
  return;
  <div style={styles}>This is a div with inline styles.</div>;
}
```

### CSS Modules for scoped CSS

- Additional setup may require
- Naming convention: `[filename].module.css`
- Encapsulated CSS within the component.

```css
// button.module.css
.button {
  background-color: blue;
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
```

```jsx
// button.jsx
import React from "react";
import styles from "./Button.module.css";
function Button() {
  return <button className={styles.button}>Click me</button>;
}
export default Button;
```

### CSS Stylesheets

- Traditional .css files imported into components.

- Classes applied via className prop.

```css
.button {
  background-color: blue;
  color: white;
  padding: 10px;
}
```

```jsx
import "./styles.css";

function Button() {
  return <button className="button">Click me</button>;
}
```

### CSS in JS

- CSS defined inside JavaScript files using tagged template literals or objects.
- Styles are scoped, dynamic, and can use JavaScript variables and logic.

```jsx
import styled from "styled-components";

const Button = styled.button`
  background-color: blue;
  color: white;
  padding: 10px;
`;

function App() {
  return <Button>Click me</Button>;
}
```

## Component Composition

Component Composition is a technique for building larger components by combining smaller, reusable components, often through the use of props and children. Instead of using inheritance, React encourages composition as the preferred way to reuse logic and UI.

- Goals:
  - Improves code reusability
  - Separates concerns
  - Easier to maintain and test

### Children Composition

- Use `props.children` to nest elements inside a parent component.

```jsx
function Modal() {
  const { children } = props;
  return <div className="modal">{children}</div>;
}
```

### Props as Configuration

- Pass a component or function via props so the parent component can control the child component

```jsx
function List() {
  const { items, renderItem } = props;
  return <ul>{items.map(renderItem)}</ul>;
}
```

### Slot Pattern (Named Children)

Allow dividing children into specific sections by passing components via props.

```jsx
function Layout({ header, content, footer }) {
  return (
    <>
      <header>{header}</header>
      <main>{content}</main>
      <footer>{footer}</footer>
    </>
  );
}
```

## Exercise

**_Note_** Use both function component and class component

### 1 Build a Traffic Light using only JSX, CSS styles, and Component Export like this picture bellow

![alt text](image.png)

### 2 Build Holy Grail

The Holy Grail layout is a famous CSS page layout that has traditionally been hard to implement. It consists of a header, footer, and three columns. The left column contains navigation items, the middle column contains the page contents, and the right column contains ads.
Implement the Holy Grail layout using just CSS. You shouldn't need to change the HTML too much.

![alt text](image-1.png)

### Requirements

- Header
  - Stretches horizontally across the whole page.
  - 60px tall.
- Columns
  - Both the left and right columns have a fixed width of 100px.
  - The center column is fluid-width.
  - All the columns should have the same height, regardless of which column is the tallest.
- Footer
  - Stretches horizontally across the whole page.
  - 100px tall.
  - The footer should be at the bottom of the page even if there is not enough content to fill up the viewport height.

### 3 Build Color palette using only JSX, CSS styles, and Component Export like this picture bellow

![alt text](image-2.png)

### 4 Build Todo list apps using only JSX, Css styles and Component Export like this picture bellow

![alt text](image-3.png)
