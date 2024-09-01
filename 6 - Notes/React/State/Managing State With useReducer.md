#### Created: 2024-08-21
#### Tags: [[React]] [[React Hooks]]
#### Links: 
[The Ultimate React Course - 189 Managing State With useReducer](https://www.udemy.com/course/the-ultimate-react-course/learn/lecture/37350954#overview)
# Managing State with useReducer

## STATE WITH useReducer

- An alternative way of setting state, ideal for complex state and related pieces of state
- Stores related pieces of state in a `state` object (Like setState() with superpowers)
- useReducer needs `reducer`: function containing all logic to update state. Decouples state logic from component
- `reducer`: pure function (no side effects!) that takes current state and action, and returns the next state
- `action`: object that describes how to update state
- `dispatch`: function to trigger state updates, by "sending" actions from event handlers to the reducer (Instead of setState())

## Code Example

```javascript
const [state, dispatch] = useReducer(reducer, initialState);

function reducer(state, action) {
  switch (action.type) {
    case 'dec':
      return state - 1;
    case 'inc':
      return state + 1;
    case 'setCount':
      return action.payload;
    default:
      throw new Error('Unknown action');
  }
}
```

## How Reducers Update State

### useReducer Syntax

```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

### State Update Flow with useReducer

Updating state in a component:
1. dispatch
2. reducer (receives CURRENT STATE and action)
3. NEXT STATE
4. RE-RENDER

- The reducer accumulates ("reduces") actions over time, similar to array.reduce()
- An action typically has this structure:
  ```javascript
  {
    type: 'updateDay',
    payload: 23
  }
  ```

### Comparison with useState

useState:
1. setState
2. NEXT (UPDATED) STATE
3. RE-RENDER

### Key Differences

- useReducer separates the state update logic (in the reducer function) from the component
- useState directly updates the state within the component
- useReducer is more suitable for complex state logic, while useState is simpler for basic state updates

### Note

Just like array.reduce(), reducers accumulate ("reduce") actions over time to produce the next state.