# Review last lesson

## React Core Overview

- JSX: Syntax extension that allows writing HTML-like code inside JavaScript.

- Components:

  - Functional components (modern standard)
  - Component composition

- `Props`: Mechanism to pass data from parent to child
- `State`: Local component state using useState
- Lifecycle (via hooks): useEffect for side effects

## State Management Options

- Local state: Simple `useState` or `useReducer`
- Context API:

  - Use for lightweight global state
  - Not ideal for frequent updates (e.g., animation states)

- `Redux`: Centralized store, middleware (e.g. Redux Toolkit)
- `Zustand` / `Jotai` / `Recoil`: Modern, simpler alternatives

## React Router & Navigation

- SPA Routing: No page reloads
- `react-router-dom`

  - `<BrowserRouter>`, `<Routes>`, `<Route>`, `<Link>`, useParams, useNavigate

- Nested routes and layout components

## Styling Approaches

- Plain CSS / CSS Modules: Scoped styles
- Styled-components / Emotion: CSS-in-JS
- Tailwind CSS: Utility-first CSS

## Tooling in React Ecosystem

**Build Tools:** CRA (legacy), Vite (modern), Next.js (SSR)

**Testing**:

- `Jest`: Unit testing
- `React Testing Library`: UI testing

**Code Quality:**

- `ESLint`: Linting rules
- `Prettier`: Code formatting

`TypeScript`:

- Interfaces & types for props
- Type-safe components

## Form in React

- `Controlled` vs. `uncontrolled` components
- Managing form state with `useState` or `useReducer`
- Validation strategies
- Form libraries: `react-hook-form`, `Formik`, `zod/yup` integration

## Form Libraries Comparison

| Library             | Bundle Size | TypeScript Support | Validation | Performance |
| ------------------- | :---------: | :----------------: | :--------: | :---------: |
| **react-hook-form** |  Small ✅   |         ✅         |  Built-in  |   🚀🚀🚀    |
| **Formik**          |   Medium    |         ✅         |    Yup     |     🚀      |
| **Native (manual)** |     N/A     |         ✅         |   Manual   |     🚀      |

- **react-hook-form**: Lightweight, fast, built-in validation, great TypeScript support.
- **Formik**: Popular, integrates with Yup for validation, good TypeScript support.
- **Native (manual)**: Full control, manual validation, minimal dependencies.

## Data Fetching with React Query

- Why you need a data-fetching library
- Introduction to `TanStack Query (React Query)`:

  - Caching
  - Loading/error states
  - Pagination

- Contrast with `useEffect` + `fetch`

```tsx
import { useQuery } from "@tanstack/react-query";

const fetchRepos = () =>
  fetch("https://api.github.com/users/octocat/repos").then((res) => res.json());

function RepoList() {
  const { data, isLoading, error } = useQuery(["repos"], fetchRepos);

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error loading repos</p>;

  return (
    <ul>
      {data.map((repo: any) => (
        <li key={repo.id}>{repo.name}</li>
      ))}
    </ul>
  );
}
```

## Component Documentation with Storybook

- Storybook is an open-source tool for:
  - Building UI components in isolation
  - Documenting reusable components
  - Testing and visually reviewing components
  - Enabling design-system collaboration between developers and designers

### Core Concepts

Storybook Structure

- `stories` are component usage examples (like test cases, but visual)
- Each story is a specific state/variant of a component

Anatomy of a Story

```tsx
import { Button } from "./Button";
import type { Meta, StoryObj } from "@storybook/react";

const meta: Meta<typeof Button> = {
  component: Button,
  title: "Components/Button",
  tags: ["autodocs"],
};
export default meta;

type Story = StoryObj<typeof Button>;

export const Primary: Story = {
  args: {
    label: "Click me",
    variant: "primary",
  },
};

export const Disabled: Story = {
  args: {
    label: "Disabled",
    disabled: true,
  },
};
```
