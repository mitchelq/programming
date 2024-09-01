#### Created: 2024-08-25
#### Tags: [[React]] [[Context API]] [[React Hooks]]
#### Links:

# Advanced Context API (Custom Provider & Hook)

Creating a custom provider with the Context API offers a significant benefit: when state changes, only the consumers will re-render. This is in contrast to keeping state in a parent component, where state changes would cause that component and all its children to re-render.

## Implementation

### 1. Create a Context File (e.g., `UserContext.js`)

```javascript
import { createContext, useState, useContext } from "react";

// Create the context
const UserContext = createContext();

// Create a custom provider
function UserProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = (userData) => {
    setUser(userData);
  };

  const logout = () => {
    setUser(null);
  };

  return (
    <UserContext.Provider value={{ user, login, logout }}>
      {children}
    </UserContext.Provider>
  );
}

// Create a custom hook for using this context
function useUser() {
  const context = useContext(UserContext);
  if (context === undefined) {
    throw new Error("useUser must be used within a UserProvider");
  }
  return context;
}

export { UserProvider, useUser };
```

### 2. Use the Provider in Your App

```jsx
import { UserProvider } from "./UserContext";

function App() {
  return (
    <UserProvider>
      <Header />
      <Main />
      <Footer />
    </UserProvider>
  );
}
```

### 3. Use the Custom Hook in Components

```jsx
import { useUser } from "./UserContext";

function Header() {
  const { user, logout } = useUser();

  return (
    <header>
      {user ? (
        <>
          <p>Welcome, {user.name}!</p>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <p>Please log in</p>
      )}
    </header>
  );
}

function LoginForm() {
  const { login } = useUser();

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

## Key Points

1. The custom provider (`UserProvider`) encapsulates the state and functions to modify it.
2. The custom hook (`useUser`) provides a convenient way to access the context and ensures it's used within the provider.
3. Components can easily consume the context using the custom hook, leading to cleaner and more maintainable code.
4. Only components that use the `useUser` hook will re-render when the context value changes.

This approach separates concerns, improves performance, and makes it easier to manage global state in your React application.