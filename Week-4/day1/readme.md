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

## useNavigate()

- Used to programmatically navigate to another route.

```jsx
import { useNavigate } from "react-router-dom";

const Login = () => {
  const navigate = useNavigate();

  const handleLogin = () => {
    navigate("/dashboard");
  };

  return <button onClick={handleLogin}>Log in</button>;
};
```

## useLocation()

- Gives you access to the current location (path, search, hash, state).

```jsx
import { useLocation } from "react-router-dom";

const ShowPath = () => {
  const location = useLocation();
  return <p>Current path: {location.pathname}</p>;
};
```

## useParams()

- Retrieves dynamic route parameters (e.g. :id in /user/:id).

```jsx
import { useParams } from "react-router-dom";

const UserDetail = () => {
  const { id } = useParams();
  return <p>User ID: {id}</p>;
};
```

## useMatch()

- Checks if the current location matches a specific path pattern.

```jsx
import { useMatch } from "react-router-dom";

const AdminBanner = () => {
  const match = useMatch("/admin/*");
  return match ? <p>Welcome, Admin</p> : null;
};
```

## useOutlet()

- Access the rendered child route component inside a layout component.

```jsx
import { useOutlet } from "react-router-dom";

const Layout = () => {
  const outlet = useOutlet();
  return (
    <>
      <nav>Sidebar</nav>
      <section>{outlet}</section>
    </>
  );
};
```

### . useNavigation() (Data Router only)

Provides info about the current navigation state (e.g. idle, submitting).

```jsx
import { useNavigation } from "react-router-dom";

const SubmitButton = () => {
  const navigation = useNavigation();
  return (
    <button disabled={navigation.state !== "idle"}>
      {navigation.state === "submitting" ? "Saving..." : "Submit"}
    </button>
  );
};
```

## Exercise 1: Setup routes

Create 3 pages — Home, About, and Contact — using createBrowserRouter, and display them inside a shared layout using`<Outlet>`.

**_Requirement_**

- Create 3 pages: Home.jsx, About.jsx, Contact.jsx.
- Create a Layout.jsx component with navigation and `<Outlet />`.
- Use `createBrowserRouter` + `RouterProvider` to define and render routes.

## Exercise 2: Nested + Dynamic Routing with createBrowserRouter

- Reuse your Home, About, Contact pages with layout and navigation
- Add nested routes under About: Team and Company pages
- Add a dynamic route under Contact: `/contact/:personId` to show individual contact details

**_Requirement_**

- Keep existing layout, pages, and routing as is.
- Under `/about`, add nested routes:
  `/about/`team → shows Team page
  `/about/company` → shows Company page
- Update About page to render nested links and an `<Outlet />` for nested content.
- Add dynamic route `/contact/:personId` rendering a new component that reads URL param and displays person info.
- Add links on Contact page to navigate to different person contacts dynamically.

## Exercise 3: Add Route Guard (Protected Route)

- Protect the Contact Person dynamic route `/contact/:personId` so only authenticated users can access it.
- Redirect unauthenticated users to a new Login page.
- Show how to implement a simple route guard with loader or redirect in React Router `v6.4+`.
- api auth `https://dummyjson.com/docs/auth`

**_Requirement_**
Create a simple Login page.

- Add a mock authentication function/state (e.g., isAuthenticated boolean).
- Use loader in the route config for `/contact/:personId` to check authentication.
- If not authenticated, redirect to`/login`.
- If authenticated, allow access to `ContactPerson`.
- Add a logout button to simulate logout and redirect to home.

## Exercise 4: Lazy-Loaded Route with API Fetch

- Add a Posts section.
- Lazy-load the Posts component using React.lazy.
- Fetch post data from `https://jsonplaceholder.typicode.com/posts.`
- View a list of posts and link to individual post detail pages via /posts/:postId.
- Initially load 10 posts.
- Add a Load More button to fetch 10 more on each click.

_**Requirement**_

- Add a new top-level route /posts with a lazy-loaded Posts.tsx component.
- Add nested dynamic route /posts/:postId for showing single post detail.
- Use loader to fetch the post data.
- Show fallback UI with Suspense.
