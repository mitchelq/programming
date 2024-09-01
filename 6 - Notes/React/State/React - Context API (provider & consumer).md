#### Created: 2024-08-24
#### Tags: [[React]] [[Context API]]
#### Links:
[[Advanced Context API (custom Provider & Hook)]]
https://react.dev/learn/passing-data-deeply-with-context
https://javascript.plainenglish.io/how-to-combine-context-providers-for-cleaner-react-code-9ed24f20225e

# React - Context API (Provider & Consumer)

The Context API is a system to pass data throughout the app **without manually passing props** down the tree. It allows us to **broadcast global state** to the entire app.

### Provider
The provider gives all child components access to the value.

### value
The value is the data that we want to make available (can be state or functions, for example setter functions).

### Consumers
All components that read the provided context value.

## Usage

Create context with the createContext function provided by React. Note that it is common practice to use an uppercase variable for context, as it is basically a component, and name it like `<subject>Context` for example UserContext for context about user authentication.

1. Create a context provider

```jsx
import { createContext } from "react";
const UserContext = createContext();
```

2. Provide value to child components

```jsx
import { useState } from "react";

function App() {
  const [user, setUser] = useState(null);

  const login = (userData) => {
    setUser(userData);
  };

  const logout = () => {
    setUser(null);
  };

  return (
    <UserContext.Provider value={{ user, login, logout }}>
      <section>
        <Header />
        <Main />
        <Footer />
      </section>
    </UserContext.Provider>
  );
}
```

If we have multiple ContextProviders, we can wrap them like this:

```jsx
<UserContext.Provider value={...}>
  <ThemeContext.Provider value={...}>
    ...
  </ThemeContext.Provider>
</UserContext.Provider>
```

3. Consume the context

We can read the context by using useContext function provided by React

```jsx
import { useContext } from "react";

function Header() {
  const { user, logout } = useContext(UserContext);
  
  return (
    <header>
      <h1>My App</h1>
      {user ? (
        <div>
          <p>Welcome, {user.name}!</p>
          <button onClick={logout}>Logout</button>
        </div>
      ) : (
        <p>Please log in</p>
      )}
    </header>
  );
}

function LoginForm() {
  const { login } = useContext(UserContext);

  const handleSubmit = (e) => {
    e.preventDefault();
    // Assume we get user data from form inputs
    login({ name: "John Doe", email: "john@example.com" });
  };

  return (
    <form onSubmit={handleSubmit}>
      {/* Login form fields */}
      <button type="submit">Login</button>
    </form>
  );
}
```

For a more advanced way of using the Context API with a custom Provider and hook, see the following note:
[[Advanced Context API (custom Provider & Hook)]]

This basic usage of the Context API allows you to share state across components without prop drilling. However, it doesn't provide the same level of encapsulation and reusability as the advanced method with custom providers and hooks.