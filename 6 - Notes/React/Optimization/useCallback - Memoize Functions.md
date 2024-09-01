#### Created: 2024-08-26
#### Tags: [[React]]
#### Links:
[[Performance Optimization Tools]]

## Overview
useCallback is a React Hook that returns a memoized callback function. This is useful for optimizing performance by preventing unnecessary re-renders of child components that depend on callback functions.

**NOTE**: useState setter functions are already omitted from the re-render of a component, so passing those as props is perfectly fine without wrapping then in a useCallback function.

## When to Use
- When passing callbacks to optimized child components that use React.memo or shouldComponentUpdate
- To prevent unnecessary re-renders in child components that depend on callback reference equality
- When you want to memoize a function for use in other hooks' dependency arrays

## Syntax
```jsx
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

## Examples for Each Use Case

### 1. Optimizing Child Component Re-renders

When passing callbacks to child components wrapped in React.memo, useCallback prevents unnecessary re-renders:

```jsx
import React, { useState, useCallback, memo } from 'react';

const ExpensiveComponent = memo(({ onClick }) => {
  console.log('ExpensiveComponent render');
  return <button onClick={onClick}>Click me</button>;
});

function App() {
  const [count, setCount] = useState(0);

  // Without useCallback, this function would be recreated on every render
  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []); // Empty dependency array means this function never changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <ExpensiveComponent onClick={handleClick} />
    </div>
  );
}
```

In this example, `handleClick` maintains the same reference across re-renders, so `ExpensiveComponent` doesn't re-render unnecessarily when `count` changes.

### 2. Stabilizing Functions in Dependency Arrays

useCallback is crucial when a function is used in a dependency array of another hook:

```jsx
import React, { useState, useCallback, useEffect } from 'react';

function SearchComponent() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);

  const fetchResults = useCallback(async () => {
    const response = await fetch(`https://api.example.com/search?q=${query}`);
    const data = await response.json();
    setResults(data);
  }, [query]); // This function only changes when query changes

  useEffect(() => {
    fetchResults();
  }, [fetchResults]); // Using the memoized function in the dependency array

  return (
    <div>
      <input 
        value={query} 
        onChange={(e) => setQuery(e.target.value)} 
        placeholder="Search..." 
      />
      <ul>
        {results.map(item => <li key={item.id}>{item.name}</li>)}
      </ul>
    </div>
  );
}
```

Here, `fetchResults` is memoized with useCallback and only changes when `query` changes, preventing unnecessary effect triggers.

### 3. Passing Stable Callbacks to Custom Hooks

When creating custom hooks that accept callbacks, useCallback ensures consistent behavior:

```jsx
import React, { useState, useCallback } from 'react';

// Custom hook that uses a callback
function useCounter(initialCount, step, onCountChange) {
  const [count, setCount] = useState(initialCount);

  const increment = useCallback(() => {
    const newCount = count + step;
    setCount(newCount);
    onCountChange(newCount);
  }, [count, step, onCountChange]);

  return [count, increment];
}

function CounterComponent() {
  const [total, setTotal] = useState(0);

  // Memoize the callback passed to the custom hook
  const handleCountChange = useCallback((newCount) => {
    setTotal(prev => prev + newCount);
  }, []);

  const [count, increment] = useCounter(0, 1, handleCountChange);

  return (
    <div>
      <p>Count: {count}</p>
      <p>Total: {total}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

In this example, `handleCountChange` is memoized to maintain a stable reference when passed to `useCounter`, ensuring consistent behavior of the custom hook.

## Key Points
- useCallback returns a memoized version of the callback that only changes if one of the dependencies has changed
- It's useful for optimizing render performance of child components
- useCallback is often used in conjunction with React.memo for child components
- The function passed to useCallback will be returned (not called) and can be used later

## Best Practices
- Use useCallback when passing callbacks to optimized child components
- Ensure the dependency array includes all values from the component scope that the callback uses
- Consider using useCallback for any function you're adding to a dependency array of another hook
- Use the React DevTools Profiler to identify unnecessary re-renders before applying useCallback

## Common Pitfalls
- Overusing useCallback for functions that don't need memoization
- Forgetting to include all necessary dependencies in the dependency array
- Using useCallback without optimizing the child components (e.g., with React.memo)
- Assuming useCallback will prevent all re-renders (it only memoizes the function reference)

## Related Concepts
- [[useMemo - Memoize Objects]]
- [[memo - Memoize Components]]
- [[useEffect]]

## Additional Notes
While useCallback can be a powerful optimization tool, it's important to use it judiciously. Unnecessary use of useCallback can actually harm performance due to the overhead of memoization. Always measure performance before and after applying useCallback to ensure it's providing a meaningful benefit.