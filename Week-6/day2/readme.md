# Review last lesson

## Design System

### Component Architecture

- [**Atomic Design**](https://atomicdesign.bradfrost.com/chapter-2/) (Atoms, Molecules, Organisms, Templates, Pages)
- Keep components **small**, **focused**, and **reusable**
- Prefer **function components** with hooks (React 18+)

#### Atomic Design in React

- Atomic Design is a methodology introduced by Brad Frost to help developers and designers build UI systems in a consistent and scalable way. It breaks down interfaces into a hierarchy of reusable components, similar to how matter is made of atoms, molecules, and so on.

**The Five Levels of Atomic Design:**

**_Atoms_**

- Smallest building blocks: buttons, labels, inputs, icons, etc.

```jsx
export const Button = ({ children, onClick }) => (
  <button onClick={onClick} className="btn">
    {children}
  </button>
);
```

**_Molecules_**

- **Groups of atoms** that form a meaningful unit.
- Still relatively simple, but they combine functionality.

```jsx
// SearchBox.tsx
import { Input } from "./Input";
import { Button } from "./Button";

export const SearchBox = ({ onSearch }) => (
  <div>
    <Input />
    <Button onClick={onSearch}>Search</Button>
  </div>
);
```

**_Organisms_**

- Complex UI sections composed of multiple `molecules` and/or `atoms`.

```jsx
// Header.tsx
import { Logo } from "./Logo";
import { Navigation } from "./Navigation";

export const Header = () => (
  <header>
    <Logo />
    <Navigation />
  </header>
);
```

### Templates

- Page-level components that define the layout and structure.

```jsx
// MainLayout.tsx
export const MainLayout = ({ header, content, footer }) => (
  <>
    {header}
    <main>{content}</main>
    {footer}
  </>
);
```

### Pages

Final compositions with real data and real content.

```jsx
export const HomePage = () => (
  <MainLayout
    header={<Header />}
    content={<WeatherWidget />}
    footer={<Footer />}
  />
);
```

**_Why Use Atomic Design?_**
Reusability: Build once, use everywhere.
Maintainability: Easy to update UI without breaking everything.
Scalability: Structure encourages modular growth.
Design-Dev consistency: Aligns component design with actual implementation.

## Project structure

### Basic Structure (Small projects / starters)

```bash
/public
/src
  /components     → Reusable UI pieces (atoms/molecules)
  /pages          → Route-level components (if using react-router)
  /hooks          → Custom React hooks
  /services       → API requests, auth, etc.
  /utils          → Pure helper functions
  /styles         → Global styles / Tailwind config
  /App.tsx
  /main.tsx
```

#### Folder Breakdown

`/components`

- Small, reusable UI elements like buttons, cards, modals.
- Can follow Atomic Design if needed, e.g., atoms/, molecules/.

`/pages`

- Pages like Home, About, Profile—mapped to routes.
- Each file/component represents one screen or view.

`/hooks`

- Custom React hooks like useLocalStorage, useToggle, useWeather.
- Encourages reuse of stateful logic across components.

`/services`

- Handles things like:
  - Fetching from REST APIs
  - Talking to Firebase/Auth0
  - Abstractions for third-party libraries

`/utils`

- Pure functions and helpers like date formatters, validators, or sorters.
- No React-specific logic—think formatDate.ts, debounce.ts.

`/assets`

- Static files: logos, icons, images, SVGs, fonts, etc.

`/styles`

- CSS/SCSS modules, Tailwind config, or global stylesheets.

`App.tsx`

- The root component.
- Usually contains the `<Router />`, `<Layout />`, and `<Routes />`.

`main.tsx`

- Your entry point where React mounts to the DOM (ReactDOM.createRoot).

### Feature-based structure

- **feature-based structure** organizes code around features or domains instead of technical layers (like components, pages, styles). This approach scales well for mid-to-large React applications, promotes encapsulation, and helps teams work more independently.

```bash
/src
  /features
    /auth
      AuthForm.tsx
      useAuth.ts
      authService.ts
      authSlice.ts
      index.ts
    /weather
      WeatherWidget.tsx
      useWeather.ts
      weatherService.ts
      index.ts
  /shared
    /components   → Generic, reusable components (e.g., Button, Modal)
    /hooks        → Reusable logic (e.g., useDebounce, useWindowSize)
    /ui           → Design system components (e.g., Card, Tabs)
    /utils        → Pure functions (e.g., formatDate, parseQuery)
    /types        → Global TypeScript types
  /layouts        → Page templates (e.g., DashboardLayout)
  /routes         → Route definitions (or use file-based routing)
  /App.tsx
  /main.tsx
```

Inside a Feature Folder

- For example, in `features/weather/`:

`WeatherWidget.tsx`: Main component for weather display
`useWeather.ts`: Encapsulated logic (fetch, state)
`weatherService.ts`: API client to Open Meteo
`weatherSlice.ts`: Redux/Zustand store (if needed)
`index.ts`: Barrel export

### Where to Use Shared Components?

Place generic, reusable UI components in `shared/components/` or `shared/ui/`:

- `Buttons`, `modals`, `inputs`, `icons`, etc.
- Anything not specific to one domain

## Monorepo or Multi-Package Setup

- A monorepo (monolithic repository) is a single Git repository that contains multiple projects or packages instead of splitting each project into its own repo.

- For React apps, a monorepo might include:
- The main web app
- Shared UI component libraries
- Utility libraries or hooks

### Why Use a Monorepo?

**Code sharing & reuse:** Easily share components, hooks, and utilities between multiple apps/packages.
**Simplified dependency management:** Manage dependencies and versions in one place.
**Consistent tooling & config:** ESLint, Prettier, testing frameworks configured once and used everywhere.
**Better collaboration:** Teams can work across packages without juggling multiple repos.
**Atomic commits** Make changes that span multiple packages atomically and consistently.

### Tools to Manage Monorepos

Several tools help manage monorepos efficiently:

| Tool                                  | Description                                                                                                                                                |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nx**                                | Powerful build system and workspace management for JS/TS, supports React, Angular, Node, etc. Has caching, code generation, and dependency graph analysis. |
| **Turborepo**                         | High-performance build system focused on speed and incremental builds. Great for React monorepos.                                                          |
| **Lerna**                             | Popular older tool for managing JavaScript monorepos. Focuses on versioning and publishing packages.                                                       |
| **Yarn Workspaces / PNPM Workspaces** | Package managers that support managing multiple packages with symlinks and centralized dependency resolution.                                              |

### Typical Monorepo Folder Structure

```bash
my-monorepo/
├── apps/
│   ├── web/           # React web app
│   ├── admin/         # Another React app (e.g. admin panel)
│   └── mobile/        # React Native app
├── packages/
│   ├── ui-library/    # Shared React UI components
│   ├── hooks/         # Shared custom hooks
│   ├── utils/         # Utility functions
│   └── api-client/    # Shared API client logic
├── node_modules/
├── package.json
├── tsconfig.json
└── workspace.config.js
```

- Each `app/package` has its own `package.json` for local dependencies.
- The root `package.json` manages workspace dependencies.
- Build tools can understand dependencies between packages (e.g., app depends on UI library).
- You can run builds/tests/lints selectively on changed packages (incremental builds).
- Changes in shared packages reflect immediately in apps without publishing.

### Benefits for React Development

- Share design systems or component libraries across multiple React apps.
- Avoid duplication of code and effort.
- Simplify upgrading shared dependencies.
- Easier to maintain consistent versions and testing standards.
- Coordinate release cycles for related packages.

### When NOT to Use Monorepo

- If your project is small or a single app, monorepo overhead might be unnecessary.
- Complex monorepos require good knowledge of tools and setup.
- Initial setup time is higher than a simple single-project repo.

### Exercise

### [Exercise 1](https://www.hackerrank.com/challenges/item-list-manager?isFullScreen=true)

### [Exercise 2](https://www.hackerrank.com/challenges/code-review-feedback/problem?isFullScreen=true)

### [Exercise 3](https://www.hackerrank.com/challenges/react-contact-form?isFullScreen=true)

### [Exercise 4](https://www.hackerrank.com/challenges/patient-medical-records?isFullScreen=true)

### [Exercise 5](https://www.hackerrank.com/challenges/blog-post/problem?isFullScreen=true)

### [Exercise 6](https://www.hackerrank.com/challenges/react-slideshow-1/problem?isFullScreen=true)

### [Exercise 7](https://www.hackerrank.com/challenges/employee-validation/problem?isFullScreen=true)

### [Exercise 8](https://www.hackerrank.com/challenges/react-word-omitter/problem?isFullScreen=true)

### [Exercise 9](https://www.hackerrank.com/challenges/cryptorank-exchange?isFullScreen=true)

### [Exercise 10](https://www.hackerrank.com/challenges/react-article-sorting?isFullScreen=true)
