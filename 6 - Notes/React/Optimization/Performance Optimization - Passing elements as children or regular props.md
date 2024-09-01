#### Created: 2024-08-26
#### Tags: [[React]]
#### Links:
- [[Performance Optimization Tools]]
- [React Official Documentation on Optimizing Performance](https://reactjs.org/docs/optimizing-performance.html)
- [React Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)

# Performance Optimization - Passing elements as children or regular props
## Overview
This note covers a specific React performance optimization technique: passing components as children or props to prevent unnecessary re-renders. This approach can significantly improve performance by ensuring that child components are created before their parent and don't re-render when the parent's state changes.

## The Problem
When a component's state changes, React re-renders that component and all its children by default. This can lead to unnecessary re-renders of complex child components, even when their props haven't changed.

## The Solution
Pass child components as props or children to their parent component. This way, the child components are created in the parent component's scope, before the parent itself is created. As a result, when the parent's state changes, the child components won't automatically re-render.

## Basic Example
```jsx
// Instead of this:
function ParentComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ExpensiveComponent />
    </div>
  );
}

// Do this:
function ParentComponent({ children }) {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      {children}
    </div>
  );
}

function App() {
  return (
    <ParentComponent>
      <ExpensiveComponent />
    </ParentComponent>
  );
}
```

## Advanced Example
```jsx
function ExpensiveComponent() {
  console.log("ExpensiveComponent rendered");
  return <div>This is an expensive component</div>;
}

function Button({ onClick, children }) {
  return <button onClick={onClick}>{children}</button>;
}

function OptimizedParent({ leftComponent, rightComponent }) {
  const [count, setCount] = useState(0);

  const incrementCount = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);

  return (
    <div>
      <h1>Count: {count}</h1>
      <Button onClick={incrementCount}>Increment</Button>
      <div style={{ display: 'flex' }}>
        <div>{leftComponent}</div>
        <div>{rightComponent}</div>
      </div>
    </div>
  );
}

function App() {
  return (
    <OptimizedParent
      leftComponent={<ExpensiveComponent />}
      rightComponent={<ExpensiveComponent />}
    />
  );
}
```

## Key Points
- Child components passed as props or children are created in the scope where they're defined, not in the parent component.
- This prevents unnecessary re-renders when the parent's state changes.
- This technique is especially useful for expensive components that don't depend on the parent's state.
- It promotes better component composition and reusability.

## Best Practices
- Use this technique for components that are expensive to render and don't depend on the parent's state.
- Combine with React.memo for function components or PureComponent for class components for additional optimization.
- Use the useCallback hook for functions passed as props to prevent unnecessary re-creation of these functions.

## Considerations
- This technique might make your component tree slightly more complex.
- It's most beneficial for expensive components. For simple components, the performance gain might be negligible.
- Always measure performance before and after optimization to ensure it's actually improving your app's performance.

## Additional Notes
While this technique can significantly improve performance, it's not always necessary for every component. Use it judiciously where you notice performance issues, particularly with complex or expensive child components that don't need to update with their parent.