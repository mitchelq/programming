#### Created: 2024-08-25
#### Tags: [[React]]
#### Links:
- [Official Documentation](https://react.dev/reference/react/useEffect)
- [Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)
# useEffect

## Overview
useEffect is a React Hook that allows you to perform side effects in functional components. It's used for operations that can't be done during rendering, such as data fetching, subscriptions, or manually changing the DOM.

## When to Use
- When you need to interact with the browser APIs or external services
- For setting up subscriptions or fetching data
- To perform side effects that depend on props or state
- For any code that needs to run after render and possibly cleanup

## Syntax
```jsx
useEffect(() => {
  // Effect code
  return () => {
    // Cleanup code (optional)
  };
}, [dependencies]);
```

## Basic Example
```jsx
import React, { useState, useEffect } from 'react';

function DocumentTitleUpdater() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]); // Only re-run the effect if count changes

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

## Advanced Example
```jsx
import React, { useState, useEffect } from 'react';

function DataFetcher({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchUser = async () => {
      try {
        setLoading(true);
        const response = await fetch(`https://api.example.com/users/${userId}`);
        if (!response.ok) throw new Error('Failed to fetch');
        const data = await response.json();
        setUser(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchUser();

    return () => {
      // Cleanup function: cancel any pending requests if component unmounts
    };
  }, [userId]); // Re-run effect if userId changes

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!user) return null;

  return <div>User: {user.name}</div>;
}
```

## Key Points
- Effects run after every render by default
- The dependency array controls when the effect runs
- Effects can return a cleanup function
- Effects are deferred until after the browser has painted

## Best Practices
- Use the dependency array to optimize performance
- Keep effects focused on a single concern
- Avoid unnecessary dependencies
- Use cleanup functions to prevent memory leaks

## Common Pitfalls
- Forgetting to include all dependencies in the dependency array
- Overusing effects for state updates (consider using other hooks or state lifting)
- Running expensive operations in effects without proper optimizations
- Not cleaning up subscriptions or timers, leading to memory leaks

## Related Concepts
- [[useLayoutEffect]]

## Additional Notes
useEffect is a powerful tool, but it's important to use it judiciously. For synchronous or layout effects that need to be run before the browser paints, consider using useLayoutEffect instead. For data fetching, the React team recommends using libraries like React Query or SWR, which provide more optimized solutions for managing server state.




