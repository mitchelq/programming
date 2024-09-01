#### Created: 2024-08-26
#### Tags: [[React]]
#### Links:
[[Performance Optimization Tools]]
## Overview
useMemo is a React Hook that memoizes the result of a computation. It's used to optimize performance by caching expensive calculations so they're only recomputed when their dependencies change.

## When to Use
- For expensive calculations that don't need to be recomputed on every render
- When you want to avoid unnecessary re-renders of child components that depend on the computed value (use together with [[memo - Memoize Components]])
- Memoizing values that are used in a dependency array of another hook (and for example avoid infinite useEffect loops)
## Syntax
```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

## Examples for Each Use Case

### 1. Expensive Calculations
```jsx
import React, { useMemo, useState } from 'react';

function PrimeCalculator() {
  const [number, setNumber] = useState(2);
  
  const isPrime = useMemo(() => {
    console.log('Calculating prime...');
    if (number <= 1) return false;
    for (let i = 2; i < Math.sqrt(number); i++) {
      if (number % i === 0) return false;
    }
    return true;
  }, [number]);

  return (
    <div>
      <input 
        type="number" 
        value={number} 
        onChange={(e) => setNumber(parseInt(e.target.value))} 
      />
      <p>{number} is {isPrime ? 'prime' : 'not prime'}</p>
    </div>
  );
}
```

### 2. Avoiding Unnecessary Re-renders of Child Components

In React, when a parent component re-renders, it typically causes all of its child components to re-render as well. This can be especially problematic when passing objects or arrays as props to memoized child components. Even if you use React.memo, the child will still re-render because JavaScript compares objects and arrays by reference, not by value.

Here's an example demonstrating the problem and how useMemo solves it:

```jsx
import React, { useState, useMemo, memo } from 'react';

// A memoized child component
const ExpensiveComponent = memo(({ data }) => {
  console.log('ExpensiveComponent render');
  return <div>{data.value}</div>;
});

function App() {
  const [count, setCount] = useState(0);

  // Problem: This object is recreated on every render
  const data = { value: 'some value' };

  // Solution: Memoize the object
  const memoizedData = useMemo(() => ({ value: 'some value' }), []);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      
      {/* This will re-render on every count change */}
      <ExpensiveComponent data={data} />
      
      {/* This will only render once */}
      <ExpensiveComponent data={memoizedData} />
    </div>
  );
}
```

In this example:
- Without useMemo, `data` is recreated on every render of App, causing ExpensiveComponent to re-render even though the data hasn't actually changed.
- With useMemo, `memoizedData` maintains the same reference across renders, so ExpensiveComponent only re-renders when the memoized value actually changes.

This pattern is particularly useful when:
1. You're passing complex objects or arrays as props to memoized child components.
2. The child component is expensive to render.
3. The data being passed doesn't need to be recalculated on every render of the parent.

### 3. Memoizing Values for Dependency Arrays
```jsx
import React, { useState, useMemo, useEffect } from 'react';

function DataFetcher() {
  const [id, setId] = useState(1);
  const [data, setData] = useState(null);

  // Memoize the options object to prevent unnecessary effect triggers
  const options = useMemo(() => ({
    headers: {
      'Content-Type': 'application/json',
      'API-Key': 'some-api-key'
    },
    body: JSON.stringify({ id })
  }), [id]);

  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch('https://api.example.com/data', options);
      const result = await response.json();
      setData(result);
    };

    fetchData();
  }, [options]); // Use the memoized options in the dependency array

  return (
    <div>
      <button onClick={() => setId(id + 1)}>Fetch Next</button>
      {data && <pre>{JSON.stringify(data, null, 2)}</pre>}
    </div>
  );
}
```

## Key Points
- useMemo returns a memoized value
- It only recomputes the memoized value when one of the dependencies has changed
- useMemo runs during rendering, so don't perform side effects in it
- If no array is provided, a new value will be computed on every render

## Best Practices
- Use useMemo for computationally expensive operations
- Ensure the dependency array includes all values that the memoized function depends on
- Don't overuse useMemo for simple calculations; it comes with its own performance cost
- Use the React DevTools Profiler to identify performance bottlenecks before applying useMemo

## Common Pitfalls
- Forgetting to include all necessary dependencies in the dependency array
- Using useMemo for simple calculations where the memoization overhead outweighs the benefits
- Performing side effects inside useMemo (use useEffect for side effects instead)
- Assuming useMemo will prevent all re-renders (it only memoizes the value, not the component)

## Related Concepts
- [[useCallback - Memoize Functions]]
- [[memo - Memoize Components]]
- [[useEffect]]

## Additional Notes
While useMemo can significantly improve performance in certain scenarios, it's important to use it judiciously. Always measure performance before and after applying useMemo to ensure it's actually improving your application's performance.