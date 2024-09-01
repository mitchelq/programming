#### Created: 2024-08-25
#### Tags: 
#### Links:
# Performance Optimization Tools


## Prevent wasted renders

A component instance only gets re-rendered in 3 different situation:
- **State Changes**
- **Context Changes**
- **Parent Re-renders**

A render does **not always means the DOM gets updated**, it just means the component function gets called. This can be an expensive operation.

A **wasted render** is a render that didn't produce any change in the DOM. This can be a problem when it happens **too frequently** or when the **component is very slow**

We have 2 main ways of optimizing our app to prevent wasted renders:
#### Memoization

Optimization technique that executes a pure function once, and saves the result in memory. Executing again with **the same arguments** will return the saved result **instead of executing the function again**. 

This will 1. prevent wasted renders and 2. improve the overall app speed / responsiveness.

[[memo - Memoize Components]]
[[useMemo - Memoize Objects]]
[[useCallback - Memoize Functions]]

#### Passing elements as children or props
[[Performance Optimization - Passing elements as children or regular props]]

#### Optimizing context re-renders
[[Optimizing context re-renders]]


## Improve app speed / responsiveness

[[useMemo - Memoize Objects]]
[[useCallback - Memoize Functions]]
[[useTransition]]

## Reduce bundle size

Use fewer 3rd-party packages
[[Code splitting and lazy loading]]








