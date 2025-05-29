# Review Last lesson

## Routing in React

## Routing

- `React Router` is the standard routing library for React. It enables single-page applications (SPAs) to navigate between views or components without reloading the page.

- `BrowserRouter`: Root of your routing configuration
- `Routes`: Set Route from the current location
- `Route`: Couples URL segments to components, and also enables data loading & mutation
- `Outlet`: Placeholder for nested route content
- `Link`: The Link component is used to navigate between routes in a React application without reloading the page.
- `NavLink`: Use NavLink to apply styles when a link is active.

## Basic Routing and navigation

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

`App.tsx`

```jsx
import { Routes, Route, Link } from "react-router-dom";
import Home from "./Home";
import About from "./About";

function App() {
  return (
    <div>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </div>
  );
}

export default App;
```

## createBrowserRouter

`createBrowserRouter` is a newer API introduced in React Router v6.4+ as part of its Data APIs. It replaces the older way of manually composing Routes and Route with JSX and instead lets you define routes as a data structure (an array of route objects).

Purpose

- Enables data loading (loader)
- Handles actions/mutations (action)
- Supports error boundaries
- Allows nested layouts and route-level code-splitting

```jsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Layout />,
    children: [
      {
        index: true,
        element: <Home />,
      },
      {
        path: "about",
        element: <About />,
      },
      {
        path: "profile/:userId",
        element: <UserProfile />,
        loader: async ({ params }) => fetch(`/api/users/${params.userId}`),
        action: async ({ request }) => {
          /* handle POST */
        },
        errorElement: <ErrorPage />,
      },
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}
```

//Layout

```jsx
import { Outlet, Link } from "react-router-dom";

export default function Layout() {
  return (
    <div>
      <h1>Dashboard</h1>
      <nav>
        <Link to="">Home</Link> | <Link to="settings">Settings</Link>
      </nav>
      <hr />
      <Outlet /> {/* 🔄 Child route content will render here */}
    </div>
  );
}
```

## Lazy-loaded routes

`Lazy-loaded routes` are a way to improve application performance by loading route-related code only when it’s needed, instead of loading everything upfront. This is especially useful in large applications where you want to reduce initial bundle size.

- When a route is lazy-loaded, the associated component or module is only fetched when the user navigates to that route. This reduces the amount of JavaScript downloaded and parsed on initial load.

```jsx
import { lazy, Suspense } from "react";
import { Route, Routes } from "react-router-dom";

const AboutPage = lazy(() => import("./pages/AboutPage"));

function AppRoutes() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/about" element={<AboutPage />} />
      </Routes>
    </Suspense>
  );
}
```

```jsx
import { createBrowserRouter, RouterProvider, lazy } from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    lazy: async () => {
      const { default: Component } = await import("./pages/HomePage");
      return { Component };
    },
  },
  {
    path: "/about",
    lazy: async () => {
      const { default: Component } = await import("./pages/AboutPage");
      return { Component };
    },
  },
]);

export default function App() {
  return <RouterProvider router={router} />;
}
```

##  Route Guards / Middleware

- Route guards (or middleware, depending on the framework) are logic you use to control access to certain routes based on conditions like authentication, roles, or feature flags.

They help protect routes and ensure users can only access pages they're allowed to.

```jsx
function RequireAuth({ children }) {
  const isAuthenticated = useAuth();
  if (!isAuthenticated) return <Navigate to="/login" />;
  return children;
}

{
  path: '/dashboard',
  element: (
    <RequireAuth>
      <DashboardPage />
    </RequireAuth>
  )
}

```

// BrowserRouter

```jsx
import React from "react";
import { Navigate, useLocation } from "react-router-dom";

function RequireAuth({ children }: { children: React.ReactNode }) {
  const isAuthenticated = useAuth();
  const location = useLocation();

  if (!isAuthenticated) {
    return <Navigate to="/login" state={{ from: location }} replace />;
  }

  return <>{children}</>;
}
```

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Dashboard from "./Dashboard";
import Login from "./Login";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/login" element={<Login />} />

        <Route
          path="/dashboard"
          element={
            <RequireAuth>
              <Dashboard />
            </RequireAuth>
          }
        />
      </Routes>
    </BrowserRouter>
  );
}
```

## Route Matching / Wildcards

- Route Matching / Wildcards in routing means how the router decides which route to render based on the current URL path, especially when you want to match patterns or catch all unmatched routes.

- Wildcards Explained
- Wildcard \* matches any path or remainder — often used for "catch-all" routes.

1 Basic Wildcard catch-all for 404

```jsx
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />

  {/* Catch all unmatched routes */}
  <Route path="*" element={<NotFound />} />
</Routes>
```

Here, if no other routes match, NotFound will render.

2 Nested Wildcard matching the rest of the URL

```jsx
<Route path="/files/*" element={<Files />} />
```

If you navigate to /files/docs/report.pdf, it still matches /files/\*.

Inside the Files component, you can use useParams or useMatch to get the rest of the wildcard path.
