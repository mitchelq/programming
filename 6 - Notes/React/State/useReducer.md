#### Created: 2024-08-25
#### Tags: [[React]] [[React Hooks]]
#### Links: [[State management]]

# React - useReducer

## Overview

`useReducer` is a React hook that provides an alternative to `useState` for managing complex state logic in functional components. It's especially useful when the next state depends on the previous one or when you have multiple sub-values in your state.

## Syntax

```javascript
const [state, dispatch] = useReducer(reducer, initialState, init);
```

- `state`: The current state
- `dispatch`: A function to dispatch actions to update the state
- `reducer`: A pure function that takes the current state and an action, and returns the new state
- `initialState`: The initial state value
- `init` (optional): A function to initialize the state lazily

## When to Use useReducer

1. Complex state logic involving multiple sub-values
2. When the next state depends on the previous one
3. When you want to optimize performance for components that trigger deep updates

## Basic Example

```javascript
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
}
```

## Benefits of useReducer

1. **Predictable state updates**: All state updates are handled in a single reducer function, making the logic more predictable and easier to test.
2. **Easier debugging**: Actions describe what happened, making it easier to understand state changes.
3. **Separation of concerns**: The state update logic is separated from the component, improving code organization.
4. **Performance optimization**: React can optimize rendering by comparing the old and new state values.

## Best Practices

1. Keep your reducer functions pure. They should not have side effects.
2. Use the action `type` property to determine how the state should change.
3. Return a new state object instead of mutating the existing state.
4. Use the `useCallback` hook to memoize the `dispatch` function if passing it to child components.
5. Consider using a `switch` statement in your reducer for clarity, especially with multiple action types.

## Advanced Usage: Lazy Initialization

You can pass a third argument to `useReducer` for lazy initialization:

```javascript
function init(initialCount) {
  return { count: initialCount };
}

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return init(action.payload);
    default:
      throw new Error();
  }
}

function Counter({initialCount}) {
  const [state, dispatch] = useReducer(reducer, initialCount, init);
  // ...
}
```

This is useful for creating the initial state lazily, especially if it involves expensive computations.

## Comparison with useState

- `useState` is simpler and sufficient for most cases of local component state.
- `useReducer` is preferable when you have complex state logic or when the next state depends on the previous one.
- `useReducer` can be more testable as you can test your reducer functions separately from your components.

Remember, while `useReducer` is powerful, it's not always necessary. Choose the right tool based on the complexity of your state management needs.