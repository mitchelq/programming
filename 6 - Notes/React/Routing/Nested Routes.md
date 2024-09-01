#### Created: 2024-08-23
#### Tags: [[React Router]] [[React]]

# Nested Routes

Nested routes in React Router are used when we want a part of the user interface to be controlled by a part of the URL. They allow us to render components inside other components based on the URL structure.

## Key Concepts

1. Nested routes are defined inside a parent route.
2. They control what component is rendered inside a larger component.
3. The `Outlet` component is used to specify where the child route should be rendered.

## Example

```jsx
import { BrowserRouter, Route, Routes } from "react-router-dom";
import Product from "./pages/Product";
import Pricing from "./pages/Pricing";
import Login from "./pages/Login";
import AppLayout from "./pages/AppLayout";
import Homepage from "./pages/Homepage";
import PageNotFound from "./pages/PageNotFound";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Homepage />} />
        <Route path="/product" element={<Product />} />
        <Route path="/pricing" element={<Pricing />} />
        <Route path="/login" element={<Login />} />
        <Route path="/app" element={<AppLayout />}>
          <Route path="cities" element={<p>list of cities</p>} />
          <Route path="countries" element={<p>list of countries</p>} />
          <Route path="form" element={<p>form</p>} />
        </Route>
        <Route path="*" element={<PageNotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

In this example, the routes under `/app` are nested routes.

## Using the Outlet Component

The `Outlet` component is used in the parent component to specify where the child routes should be rendered:

```jsx
import { Outlet } from "react-router-dom";
import AppNav from "./AppNav";
import Logo from "./Logo";
import styles from "./Sidebar.module.css";

function Sidebar() {
  return (
    <div className={styles.sidebar}>
      <Logo />
      <AppNav />

      <Outlet />

      <footer className={styles.footer}>
        <p className={styles.copyright}>
          &copy; {new Date().getFullYear()} by WorldWise
        </p>
      </footer>
    </div>
  );
}
```

## Navigation Between Nested Routes

Use `NavLink` components to create navigation between nested routes:

```jsx
<NavLink to="cities">Cities</NavLink>
<NavLink to="countries">Countries</NavLink>
```

## Benefits of Nested Routes

1. Allows for more complex UI structures
2. Keeps related routes together
3. Enables dynamic rendering of components based on URL
4. Similar to a tabs component, but managed by the URL instead of state

Remember: Nested routes are not just routes with multiple parts in the path. They specifically refer to routes that render components inside other components based on the URL structure.


For nested routes that have an index that should be redirected to a subpage we can use the <Navigate /> component so the URL gets updated correctly, like this:
```jsx
import { BrowserRouter, Navigate, Route, Routes } from "react-router-dom";

<Route path="app" element={<AppLayout />}>
    <Route
	    index
        element={<Navigate to="cities" replace={true} />}
    />
    <Route
        path="cities"
        element={<CityList cities={cities} isLoading={isLoading} />}
    />
</Route>
```

**NOTE**: The `replace` keyword makes sure we can still go back and the route actually replaces the current element in the history stack instead of being forwarded.