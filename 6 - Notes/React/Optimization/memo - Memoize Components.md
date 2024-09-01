#### Created: 2024-08-26
#### Tags: [[React]]
#### Links:
[[Performance Optimization Tools]]
# memo - Memoize Components

- Used to create a component that will **not re-render when its parent re-renders**, as long as the **props stay the same between renders**
- **Only affects props!** A memoized component will still re-render when its **own state changes** or when a **context that it's subscribed to changes** 
- Only makes sense when the component is **heavy** (slow / expensive), **re-renders often**, and does so **with the same props** 

## Overview
React.memo is a higher-order component that memoizes the rendered output of a component to optimize performance by preventing unnecessary re-renders.

## When to Use
- For components that render often with the same props
- When dealing with large lists of items
- In cases where re-renders are noticeably impacting performance
- For pure functional components (components that always render the same output for the same props)

## Syntax
```jsx
const MemoizedComponent = React.memo(Component, [arePropsEqual]);
```

## Basic Example

We just wrap the whole component in the memo function and store it in a constant

```jsx
import React, { memo } from 'react';

const ExpensiveComponent = memo(function ExpensiveComponent({ prop1, prop2 }) {
  // Expensive rendering logic here
  return (
    <div>
      <h1>{prop1}</h1>
      <p>{prop2}</p>
    </div>
  );
});

export default ExpensiveComponent;
```

## Advanced Example
```jsx
import React, { memo, useState, useCallback } from 'react';

const ItemList = memo(function ItemList({ items, onItemClick }) {
  console.log('ItemList rendered');
  return (
    <ul>
      {items.map(item => (
        <li key={item.id} onClick={() => onItemClick(item.id)}>
          {item.name}
        </li>
      ))}
    </ul>
  );
});

function App() {
  const [items, setItems] = useState([
    { id: 1, name: 'Item 1' },
    { id: 2, name: 'Item 2' },
  ]);
  const [count, setCount] = useState(0);

  const handleItemClick = useCallback((id) => {
    console.log(`Item ${id} clicked`);
  }, []);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ItemList items={items} onItemClick={handleItemClick} />
    </div>
  );
}

export default App;
```

## Key Points
- memo only checks for prop changes by default
- It performs a shallow comparison of props
- memo can accept a custom comparison function as a second argument
- Memoization comes with a small performance cost, so it's not always beneficial for simple components

## Best Practices
- Use memo for components that re-render frequently with the same props
- Combine memo with useCallback for function props to ensure they don't change on every render
- Use the React DevTools Profiler to identify components that would benefit from memoization
- Consider using useMemo for expensive computations within a component

## Common Pitfalls
- Overusing memo on simple components, which can lead to decreased performance
- Forgetting to memoize callback functions or objects passed as props, causing unnecessary re-renders
- Relying on memo to fix performance issues caused by poor state management
- Not considering that memo only does a shallow comparison of props by default

## Related Concepts
- [[useMemo - Memoize Objects]]
- [[useCallback - Memoize Functions]]

## Additional Notes
While memo can significantly improve performance in certain scenarios, it's not a silver bullet for all performance issues. Always measure the impact of your optimizations using profiling tools. In some cases, rethinking your component structure or state management might be more beneficial than applying memo.

## Snippet(s)
###### App.jsx
```jsx
import React, { memo, useState } from 'react';

const ExpensiveComponent = memo(function ExpensiveComponent({ data }) {
  console.log('ExpensiveComponent rendered');
  return <div>{/* Expensive rendering logic */}</div>;
});

function App() {
  const [count, setCount] = useState(0);
  const data = { /* ... */ };

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ExpensiveComponent data={data} />
    </div>
  );
}

export default App;
```