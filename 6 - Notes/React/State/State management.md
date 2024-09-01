#### Created: 2024-08-25
#### Tags:  [[React]]
#### Links:

# React - State Management

## State Placement Options

| Where to place state? | Tools                                            | When to use?                        |
| --------------------- | ------------------------------------------------ | ----------------------------------- |
| Local component       | [[useState]], [[useReducer]], or useRef          | Local state                         |
| Parent component      | [[useState]], [[useReducer]], or useRef          | Lifting up state                    |
| Context               | [[Context API]] + [[useState]] or [[useReducer]] | Global state (preferably UI state)  |
| 3rd-party library     | Redux, React Query, SWR, Zustand, etc.           | Global state (remote or UI)         |
| URL                   | React Router                                     | Global state, passing between pages |
| Browser               | Local storage, session storage, etc.             | Storing data in user's browser      |
## Types of State

### State Accessibility

| Local State                                       | Global State                                     |
| ------------------------------------------------- | ------------------------------------------------ |
| Needed only by one or few components              | Might be needed by many components               |
| Only accessible in component and child components | Accessible to every component in the application |

### State Domain

| Remote State                                           | UI State                                          |
| ------------------------------------------------------ | ------------------------------------------------- |
| All application data loaded from a remote server (API) | Everything else                                   |
| Usually asynchronous                                   | Theme, list filters, form data, etc.              |
| Needs re-fetching + updating                           | Usually synchronous and stored in the application |

## Where to place State

### Local component
- **When to use:** For local state. Only used by the component
- **Tools:** [[useState]], [[useReducer]], useRef

### Parent component
- **When to use:** If state needs to be lifted up (for use in multiple children)
- **Tools:** [[useState]], [[useReducer]], useRef

### Context
- **When to use:** For Global state (preferably UI state)
- **Tools:** [[Context API]] combined with useState or [[useReducer]]

### URL
- **When to use:** For Global state that is passed between pages. Display state (like filters, etc)
- **Tools:** React Router

### Browser
- **When to use:** For storing data in the user's browser
- **Tools:** Local Storage, Session Storage, etc.

### 3rd party tools
- **When to use:** For Global state (remote or UI state)
- **Tools:**
  - Redux, Zustand, etc.
  - Specialized for remote state: 
	  - React Query 
	  - RTK (React Toolkit) Query
	  - SWR

## Additional Notes

- For UI State, tools like [[useState]], [[useReducer]], useRef, Context API, and various state management libraries can be used depending on the scope and complexity of the state.
- For Remote State, while basic tools like fetch + [[useEffect]] + [[useState]]/[[useReducer]] can be used (especially in smaller applications), specialized tools like React Query, SWR, and RTK Query are highly effective in handling remote state management.
- The choice of tool often depends on the size and complexity of the application, as well as the specific requirements of the state being managed.