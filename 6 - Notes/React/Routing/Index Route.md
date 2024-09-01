#### Created: 2024-08-23
#### Tags: [[React]] [[React Router]]
# Index Route

Index routes in React Router are used to specify a default child route when the parent route is matched but none of its child routes are.

## Key Concepts

1. Index routes are defined using the `index` prop instead of a `path` prop.
2. They render when the parent route matches but none of its children do.
3. Useful for displaying default content in nested route structures.

## Example

```jsx
import { BrowserRouter, Route, Routes } from "react-router-dom";
import AppLayout from "./pages/AppLayout";
import Homepage from "./pages/Homepage";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route index element={<Homepage />} />
        <Route path="/app" element={<AppLayout />}>
          <Route index element={<p>Default app content</p>} />
          <Route path="cities" element={<p>list of cities</p>} />
          <Route path="countries" element={<p>list of countries</p>} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
```

In this example:
- The root route (`/`) uses an index route to render the `Homepage` component by default.
- The `/app` route has an index route that renders default content when no child route is matched.

## Use Cases

1. Providing a default view for a parent route
2. Avoiding empty states in nested route structures
3. Simplifying route definitions by eliminating the need for catch-all routes

## Benefits of Index Routes

1. Improves user experience by always showing relevant content
2. Simplifies route definitions
3. Allows for more intuitive URL structures

Remember: Index routes are a way to specify what should be rendered by default in a nested route structure, improving the overall user experience of your React application.





