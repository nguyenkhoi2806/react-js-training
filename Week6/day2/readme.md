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
/src
  /components     → Reusable UI pieces (atoms/molecules)
  /pages          → Route-level components (if using react-router)
  /hooks          → Custom React hooks
  /services       → API requests, auth, etc.
  /utils          → Pure helper functions
  /assets         → Images, fonts, icons
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
