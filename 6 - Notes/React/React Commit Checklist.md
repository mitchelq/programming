#### Created: 2024-08-21
#### Tags: [[React]] [[Checklists]]
# React Commit Checklist

## 1. State Management

### 1.1 Deciding on State

- [ ]  Does the data change? If NO → Use a regular const variable
- [ ]  Can it be computed from existing state or props? If YES → [[Derive State]]
- [ ]  Does it need to re-render the component? If NO → Use [[useRef]]
- [ ]  Otherwise → Create a new piece of state

### 1.2 Updating State

- [ ]  Does setting state rely on the current state? If YES → Use a callback function
- [ ]  Is the state update triggered by an event? If YES → Use an event handler

### 1.3 State Placement

- [ ]  Is it only used by this component? If YES → Keep it in the component
- [ ]  Is it used by a child component? If YES → Pass to child via props
- [ ]  Is it used by sibling components? If YES → Lift state to common parent
- [ ]  Is it used across the app? If YES → Consider [[Global State Management]]

## 2. Component Design

### 2.1 Splitting Components

Consider splitting if:

- It creates a logical separation of content or layout
- Part of the component is reusable
- The component does too many different things
- There are too many props
- There is too much state or too many effects
- The code is confusing or too complex
### 2.2 Component API

- [ ]  Are props set up as a clear API? Is it usable if you don’t know the code inside the component?
- [ ]  Is the component usable without knowing its internal code?

## 3. Naming Conventions

- [ ]  Functions passed as props: Start with "on" (e.g., onAddItem)
- [ ]  Event handlers in components: Start with "handle" (e.g., handleSubmit)
- [ ]  Component names: Describe what it does or displays
- [ ]  Custom hooks: Start with "use" (e.g., useFetch)

## 4. Render Logic

- [ ]  Is the render logic pure? (Same props always return same output)
- [ ]  Are there any side effects in the render? If YES → Move to an effect or event handler

Avoid in render logic:

- [ ]  Network calls
- [ ]  Timers
- [ ]  DOM API usage
- [ ]  Mutating external objects/variables
- [ ]  Updating state

## 5. Effects

- [ ]  Does each effect do only one thing?
- [ ]  Are cleanup functions implemented where necessary?

Cleanup checklist:

- [ ]  Cancel HTTP requests
- [ ]  Cancel API subscriptions
- [ ]  Clear timers
- [ ]  Remove event listeners

## 6. Code Reuse

### 6.1 UI Reuse

- [ ]  Can this UI be reused? If YES → [[Creating a React Component]]

### 6.2 Logic Reuse

- [ ]  Does the logic use hooks?
    - If YES → [[Creating a Custom Hook]]
        - [ ]  Ensure the hook has one responsibility
        - [ ]  Name starts with "use"
    - If NO → [[Creating a Regular Function]]

## 7. Performance Optimization

- [ ]  Are expensive calculations memoized? Consider [[useMemo - Memoize Objects]]
- [ ]  Are callback functions memoized? Consider [[useCallback - Memoize Functions]]
- [ ]  For class components: Is [[shouldComponentUpdate]] implemented correctly?
- [ ]  For function components: Is [[memo - Memoize Components]] used where appropriate?

## 8. Final Checks

- [ ]  Are all unused variables and imports removed?
- [ ]  Are prop types or TypeScript types defined?
- [ ]  Is the code formatted consistently?
- [ ]  Are there appropriate comments for complex logic?
- [ ]  Are constants placed outside the component when possible?

# Reference





