#### Created: 2024-08-30
#### Tags: [[React]] [[Overview]] [[Glossary]]
#### Links: [[React Components]] [[React Hooks]] [[React State Management]] [[React Performance Optimization]]

# React Overview and Glossary

## Overview
This note provides a comprehensive overview of React concepts, serving as both a table of contents and a brief glossary. Each entry includes a concise description to quickly refresh your memory or guide you to more detailed notes.

## Core Concepts

### 1. React Basics
React is a JavaScript library for building user interfaces. It uses a component-based architecture and a virtual DOM for efficient rendering.

### 2. JSX
JSX is a syntax extension for JavaScript, used with React to describe what the UI should look like. It allows you to write HTML-like code in your JavaScript files.

### 3. Components
Components are the building blocks of React applications. They can be functional (using hooks) or class-based, and can be composed to create complex UIs.

### 4. Props
Props (short for properties) are a way to pass data from parent to child components. They are read-only and help make your components reusable.

### 5. State
State represents the internal data of a component that can change over time. In functional components, state is managed using the useState hook.

## Hooks

### 6. useState
useState is a hook that allows functional components to have state. It returns a stateful value and a function to update it.

### 7. useEffect
useEffect is used for side effects in functional components. It runs after every render and can be used for data fetching, subscriptions, or manually changing the DOM.

### 8. useContext
useContext provides a way to pass data through the component tree without having to pass props down manually at every level.

### 9. useRef
useRef returns a mutable ref object that persists for the full lifetime of the component. It's commonly used to access DOM elements directly.

### 10. useMemo
useMemo is used to memoize expensive computations so that they are only recomputed when one of their dependencies changes.

### 11. useCallback
useCallback is similar to useMemo, but it's used to memoize functions instead of values. It's useful for optimizing child component re-renders.

## Advanced Concepts

### 12. React Router
React Router is a standard library for routing in React. It enables navigation among views in a React application, allowing for a single-page app experience.

### 13. Context API
The Context API provides a way to pass data through the component tree without having to pass props down manually at every level.

### 14. Higher-Order Components (HOCs)
HOCs are functions that take a component and return a new component with some added functionality. They're used for code reuse, logic abstraction, and state manipulation.

### 15. Render Props
Render Props is a technique for sharing code between React components using a prop whose value is a function.

### 16. Error Boundaries
Error Boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI.

## State Management

### 17. Redux
Redux is a predictable state container for JavaScript apps. It helps you write applications that behave consistently and are easy to test.

### 18. MobX
MobX is a simple, scalable state management solution. It makes state management simple and scalable by transparently applying functional reactive programming.

### 19. Recoil
Recoil is an experimental state management library for React apps. It provides several capabilities that are difficult to achieve with Redux.

## Performance Optimization

### 20. React.memo
React.memo is a higher-order component that can be used to wrap functional components to prevent unnecessary re-renders.

### 21. useCallback and useMemo for optimization
These hooks are used to optimize performance by memoizing functions and values, respectively.

### 22. Code Splitting
Code splitting is a technique to split your code into small chunks which you can then load on demand.

## Testing

### 23. Jest
Jest is a delightful JavaScript Testing Framework with a focus on simplicity. It works with projects using Babel, TypeScript, Node, React, Angular, Vue and more.

### 24. React Testing Library
React Testing Library is a very light-weight solution for testing React components. It provides light utility functions on top of react-dom and react-dom/test-utils.

## Additional Tools

### 25. Create React App
Create React App is an officially supported way to create single-page React applications. It offers a modern build setup with no configuration.

### 26. Next.js
Next.js is a React framework that enables functionality such as server-side rendering and generating static websites for React based web applications.

This overview provides a quick reference to key React concepts. Each topic can be expanded into its own detailed note for in-depth understanding and examples.