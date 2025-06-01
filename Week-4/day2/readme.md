# Review last exercise

## Testing in React

### What is Testing in React?

Testing in React means verifying that your components, hooks, and logic behave as expected. It involves checking rendering, interactions, props, side effects, and data flow using tools like Jest and React Testing Library (RTL).

### Why Test React Apps?

- Catch bugs early before they hit production
- Ensure UI consistency as you refactor
- Document component behavior clearly
- Prevent regressions during feature updates
- Improve confidence when shipping code

### When to Test?

- As you build: write tests alongside your features (Test-Driven or side-by-side)
- Before refactoring: capture current behavior to avoid regressions
- After a bug fix: reproduce the bug in a test to prevent it from reoccurring
- During CI/CD: run all tests automatically before deployments

### Tools?

- Jest – test runner, assertions, mocking
- React Testing Library – test what users see/interact with
- MSW (Mock Service Worker) – mock API calls in tests

### What should test in react apps ?

#### Component Rendering

- Does the component render without crashing?
- Does it display the correct content based on props or state?

```jsx
// UserCard.tsx
export const UserCard = ({ name }: { name: string }) => <h1>{name}</h1>;

// UserCard.test.tsx
import { render, screen } from "@testing-library/react";
import { UserCard } from "./UserCard";

test("renders user name", () => {
  render(<UserCard name="Alice" />);
  expect(screen.getByText("Alice")).toBeInTheDocument();
});
```

#### User Interactions

- Does clicking a button perform the expected action?
- Are inputs updating the state or submitting correctly?

```jsx
export const Counter = () => {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
};

import { render, screen, fireEvent } from "@testing-library/react";
import { Counter } from "./Counter";

test("increments counter", () => {
  render(<Counter />);
  fireEvent.click(screen.getByText(/Count:/));
  expect(screen.getByText("Count: 1")).toBeInTheDocument();
});
```

#### Conditional Rendering

Does the UI update correctly based on different props or states?

```jsx
// LoadingMessage.tsx
export const LoadingMessage = ({ isLoading }: { isLoading: boolean }) =>
  isLoading ? <p>Loading...</p> : <p>Done</p>;

// LoadingMessage.test.tsx
test("shows loading message", () => {
  render(<LoadingMessage isLoading={true} />);
  expect(screen.getByText("Loading...")).toBeInTheDocument();
});
```

#### Props and State Changes

- Does the component behave correctly with different prop values?
- Does internal state update properly after interactions?

```jsx
export const Child = ({ text }: { text: string }) => {
  return <p>{text}</p>;
};

import { useState } from "react";
import { Child } from "./Child";

export const Parent = () => {
  const [message, setMessage] = useState("Hello");

  return (
    <div>
      <button onClick={() => setMessage("Goodbye")}>Change Message</button>
      <Child text={message} />
    </div>
  );
};
```

```jsx
import { render, screen, fireEvent } from "@testing-library/react";
import { Parent } from "./Parent";

test("updates child text when parent state changes", () => {
  render(<Parent />);

  expect(screen.getByText("Hello")).toBeInTheDocument();

  fireEvent.click(screen.getByText("Change Message"));

  expect(screen.getByText("Goodbye")).toBeInTheDocument();
});
```

#### Side Effects (useEffect)

- Is data fetched correctly on mount?
- Are subscriptions and timers cleaned up properly?

```jsx
export const FetchPosts = () => {
  const [posts, setPosts] = useState<string[]>([]);
  useEffect(() => {
    fetch("/posts")
      .then(res => res.json())
      .then(data => setPosts(data));
  }, []);
  return <ul>{posts.map(p => <li key={p}>{p}</li>)}</ul>;
};

global.fetch = vi.fn(() =>
  Promise.resolve({ json: () => Promise.resolve(["post1", "post2"]) })
) as any;

test("fetches and displays posts", async () => {
  render(<FetchPosts />);
  expect(await screen.findByText("post1")).toBeInTheDocument();
});

```

#### Route Handling and Guards

- Are the correct components rendered for specific routes?
- Is protected content blocked from unauthenticated users?

```jsx
// ProtectedRoute.tsx
import { Navigate } from "react-router-dom";
export const ProtectedRoute = ({ isAuth, children }: any) =>
  isAuth ? children : <Navigate to="/login" replace />;

// ProtectedRoute.test.tsx
test("redirects unauthenticated user", () => {
  render(
    <MemoryRouter initialEntries={["/dashboard"]}>
      <Routes>
        <Route path="/login" element={<p>Login Page</p>} />
        <Route
          path="/dashboard"
          element={
            <ProtectedRoute isAuth={false}>
              <p>Dashboard</p>
            </ProtectedRoute>
          }
        />
      </Routes>
    </MemoryRouter>
  );
  expect(screen.getByText("Login Page")).toBeInTheDocument();
});
```

#### Custom Hooks

- Does the hook return the right data or state?
- Do side effects work as expected?

```jsx
// useToggle.ts
export const useToggle = (init = false) => {
  const [value, setValue] = useState(init);
  const toggle = () => setValue(v => !v);
  return [value, toggle] as const;
};

// useToggle.test.tsx
const TestHook = () => {
  const [value, toggle] = useToggle();
  return <button onClick={toggle}>{value ? "On" : "Off"}</button>;
};

test("toggles value", () => {
  render(<TestHook />);
  fireEvent.click(screen.getByText("Off"));
  expect(screen.getByText("On")).toBeInTheDocument();
});

```

### Mock in React testing

#### What is Mocking?

Mocking is the practice of replacing real dependencies (functions, modules, APIs, etc.) with fake versions that simulate their behavior in a controlled way.

#### Why Use Mocks?

- To isolate the component or logic under test.
- To avoid external side effects, like API requests or database access.
- To simulate edge cases (e.g. slow responses, errors).
- To improve test reliability and speed.

#### How to Mock in React Testing

- There are several ways to mock depending on what you're mocking:

##### Mock a module (like an API helper)

```jsx
export const fetchUser = () => fetch("/user").then((res) => res.json());


import * as api from './api';
jest.mock('./api'); // this replaces the real module

(api.fetchUser as jest.Mock).mockResolvedValue({ name: 'John' });
```

##### Mock a component

```jsx
// Original heavy component
export const Chart = () => {
  // expensive render
  return <div>Chart</div>;
};

// In test
jest.mock("./Chart", () => ({
  Chart: () => <div>MockChart</div>,
}));
```

##### Mock a hook or utility

```jsx
jest.mock("react-router-dom", () => ({
  ...jest.requireActual("react-router-dom"),
  useNavigate: () => jest.fn(),
}));
```

#### When to Use Mocks

Use mocking when:

- You depend on a slow, external, or unreliable resource (like APIs).
- You're unit testing and want to focus on just one function/component.
- You want to simulate error conditions or rare scenarios.
- You're testing logic, not rendering, of a component that uses external tools.

## Exercise

### Write tests for the exercises from Week 1 to Week 4
