#### Created: 2024-08-25
#### Tags: 
#### Links:
- [[useReducer]]
- [Official Documentation](https://react.dev/reference/react/useState)
- [State: A Component's Memory](https://react.dev/learn/state-a-components-memory)
# useState

#### Created: 2024-08-26
#### Tags: [[React]] [[State management]] [[React Hooks]]

## Overview
useState is a React Hook that allows functional components to manage state. It returns an array containing the current state value and a function to update it.
## Remember
State is immutable. If working with objects or arrays, never modify the state but instead return a new object or array!
## When to Use
- When you need to add state to a functional component
- For managing simple, independent pieces of state
- When state updates are straightforward assignments

## Syntax
```jsx
const [state, setState] = useState(initialState);
```

## Basic Example
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

## Advanced Example
```jsx
import React, { useState } from 'react';

function Form() {
  const [form, setForm] = useState({
    name: '',
    email: '',
    age: 0
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm(prevForm => ({
      ...prevForm,
      [name]: value
    }));
  };

  return (
    <form>
      <input
        name="name"
        value={form.name}
        onChange={handleChange}
        placeholder="Name"
      />
      {/* Similar inputs for email and age */}
    </form>
  );
}
```

## Key Points
- useState preserves state between re-renders
- It can hold any type of value (primitives, objects, arrays)
- The setter function can accept a value or a function

## Best Practices
- Use multiple useState calls for unrelated state items
- Use the functional update form when new state depends on old state
- Keep state as local as possible to the components that need it

## Common Pitfalls
- Directly mutating state instead of using the setter function
- Forgetting that setState is asynchronous
- Using a single useState for complex, nested state structures

## Related Concepts
- [[useReducer]]
- [[State management]]

## Additional Notes
For complex state logic or when state depends on previous state, consider using useReducer instead.
