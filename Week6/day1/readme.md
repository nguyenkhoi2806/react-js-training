# Review last lesson

## React 19

### What’s New in React 19?

React 19 introduces several new features and improvements that enhance the developer experience and performance of React applications

### Concurrent Features in React 19

#### What is Concurrent Mode

- Concurrent Mode lets `React` prepare multiple UI updates simultaneously without blocking the browser.
- It makes `React` apps more responsive and smooth, especially during heavy rendering or data fetching.
- `React` can pause, abort, or resume work as needed — improving user experience.

#### Why is it important?

- UI stays interactive even while React is rendering complex parts.
- Supports `interruptible rendering`, so React can prioritize urgent updates like `typing` or `clicks`.
- Enables new features like transitions, where UI updates can be deferred smoothly.

#### How React 19 improves it

- React 19 stabilizes concurrent features making them easier to adopt.
- Works seamlessly with new hooks like `use()`, `useOptimistic()`, and `Suspense`.
- Better integration with server components and streaming.

### Automatic Batching in React 19

#### What is batching?

- Batching means grouping multiple state updates into one render for better performance.
- Before React 18, updates inside React event handlers were batched, but updates inside async callbacks (like promises, timeouts, fetches) were not.

#### What changed in React 19?

- React 19 extends automatic batching to all updates, including inside async code.
- This means even state updates from promises, setTimeout, or native event handlers get batched together automatically.
- Result: fewer renders, faster UI updates, and smoother user experience.

**Example:**

```jsx
function Example() {
  const [count, setCount] = React.useState(0);
  const [text, setText] = React.useState("");

  function handleClick() {
    setTimeout(() => {
      setCount((c) => c + 1);
      setText("Updated");
      // In React 19, these two updates batch into one render automatically
    }, 1000);
  }

  return (
    <div>
      <p>Count: {count}</p>
      <p>Text: {text}</p>
      <button onClick={handleClick}>Update</button>
    </div>
  );
}
```

### `use()` Hook

**What is it?**

- The use() hook lets you "await" a promise inside a React component — without needing `useEffect`, `useState`, or manually tracking loading/error states.
- It works in both Client Components (for Suspense boundaries) and Server Components, enabling cleaner async code.

**Why use it?**

- Simplifies async logic — no more juggling useEffect + loading states.
- Cleaner JSX — you can write code that looks synchronous but handles async under the hood.
- Perfect for fetching data, lazy-loading modules, or waiting for transitions.

Example:

```jsx
function User() {
  const user = use(fetchUser());
  return <p>Hello, {user.name}</p>;
}
```

No `useEffect`, no loading states — just direct usage!

Example: Suspense with Loading UI

```jsx
function App() {
  return (
    <Suspense fallback={<p>Loading user...</p>}>
      <User />
    </Suspense>
  );
}
```

React automatically suspends rendering until the promise resolves, and shows the fallback in the meantime.

### Actions for Forms

**What is it?**

- React 19 now allows you to pass an `async or server function` directly to the action prop of a `<form>` element. This means you no longer need to handle onSubmit, prevent default behavior, extract form data, or manage local state manually — React handles it all under the hood.

**Why is it useful?**

- Less boilerplate: You don’t need to write `onSubmit`, `e.preventDefault()`, or `new FormData()`.
- Cleaner components: The form logic lives closer to where it's used — directly in the JSX.
- Server-ready: Works well with Server Components and server actions in frameworks like `Next.js` or `Remix`.

Example:

```jsx
function MyForm() {
  async function submit(data) {
    console.log(data);
  }

  return (
    <form action={submit}>
      <input name="email" />
      <button type="submit">Send</button>
    </form>
  );
}
```

### useFormStatus()

- **What is it?**

A React hook that lets you check if a form is currently submitting or has encountered an error. It works inside a child component of a form that uses an action.

- **Why use it?**

It helps you update the UI based on the form state — for example, disabling the submit button or showing a loading spinner while the form is submitting.

- Key return values:

- `pending` – true if the form is currently submitting
- `data` – submitted form data
- `method` – form method (e.g., POST)
- `action` – function passed to the form
- `error` – any error that occurred during submission

```jsx
function MyForm() {
  async function submit(formData) {
    await saveToServer(formData);
  }

  return (
    <form action={submit}>
      <input name="email" />
      <SubmitButton />
    </form>
  );
}

function SubmitButton() {
  const { pending } = useFormStatus();
  return (
    <button type="submit" disabled={pending}>
      {pending ? "Sending..." : "Send"}
    </button>
  );
}
```

### useOptimistic() — Instant UI Feedback

- **What is it ?**

- `useOptimistic()` is a React 19 hook that lets you immediately update the UI with expected data before the server confirms the change.

- This is called optimistic UI — it makes your app feel faster and more responsive by assuming success while waiting for a server response.

- **Why use it ?**

- Faster feeling UI – users see updates instantly.
- Less loading spinners – show the result now, then correct if needed.
- More modern UX – like Twitter showing a new tweet right away before saving it to the server.

- **How does it work?**

- You pass:

1 The current state
2 A function that returns the “optimistic” version of the state
3 Optionally, a server action that will finalize the update

- React will:

- Immediately apply the optimistic update
- Later update the state based on the actual result (or error)

```jsx
function Comments({ comments }) {
  const [optimisticComments, addOptimisticComment] = useOptimistic(
    comments,
    (currentComments, newComment) => [...currentComments, newComment]
  );

  async function addCommentAction(formData) {
    const newComment = formData.get("comment");
    addOptimisticComment({ text: newComment });
    await saveCommentToServer(newComment);
  }

  return (
    <form action={addCommentAction}>
      <input name="comment" />
      <button type="submit">Add</button>

      <ul>
        {optimisticComments.map((c, i) => (
          <li key={i}>{c.text}</li>
        ))}
      </ul>
    </form>
  );
}
```

### React Compiler (Preview)

**What is it?**

- The React Compiler is a new experimental tool in React 19 that automatically transforms your React code at build time to optimize performance.
- Instead of relying on runtime helpers like useMemo, useCallback, or React.memo, the compiler rewrites your code so React components run faster by default.

**Why use it?**

- Less boilerplate — You don’t have to manually wrap components or functions with React.memo or use memo hooks.
- Better performance — The compiler analyzes your code and removes unnecessary re-renders and optimizes updates.
- Simpler code — Write normal React components and let the compiler handle the optimization behind the scenes.

**How does it work?**

- The compiler parses your React source code.
- It automatically adds optimizations like memoization and inline caching.
- It reduces the amount of work React needs to do during rendering.
- It’s built to work seamlessly with React’s new concurrent rendering and `Suspense features`.

**Example**

- Instead of writing:

```jsx
const MyComponent = React.memo(function MyComponent(props) {
  // component code
});
```

- You can write:

```jsx
function MyComponent(props) {
  // component code
}
```
