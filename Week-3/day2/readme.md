# Review last lesson

## Custom Hooks and Pattern Rendering in React

### Custom Hooks

- Custom Hooks are hooks you create yourself by combining built-in hooks.
- Purpose: To reuse logic across multiple components and keep code clean and maintainable.

#### Why use Custom Hooks?

- When multiple components share the same logic.
- To separate logic from UI.
- To increase code reusability and maintainability.

#### How to create a Custom Hook

- Name the hook starting with use.
- Use React hooks inside your custom hook.
- Return values or functions you want to expose.

```jsx
import { useState, useEffect } from "react";

function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }
    window.addEventListener("resize", handleResize);

    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return width;
}
```
