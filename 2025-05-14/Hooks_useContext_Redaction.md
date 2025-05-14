# Understanding React Hooks and Deep Dive into useContext

## What are React Hooks?

React Hooks are functions introduced in version 16.8 that allow functional components to use state and side effects. They simplify component logic, reducing boilerplate from class components and enabling more readable code. Hooks promote functional programming in React.

## What is useContext?

`useContext` is a React Hook that lets you read and subscribe to context from your component. It provides a way to access and manage state that needs to be shared across multiple components. This hook simplifies data sharing without the need for prop drilling.

## What is it used for?

`useContext` is primarily used for passing data deeply into the component tree without manually passing props at every level. It's useful for sharing things like theme settings, user authentication status, or simple global state. It helps avoid the cumbersome practice of prop drilling.

## How does it work?

First, you create a context object using `React.createContext(defaultValue)`. Then, you wrap a part of your component tree with a `<YourContext.Provider value={value}>`. Any component within this provider can then access the context's value using the `useContext(YourContext)` hook. Components using `useContext` will automatically re-render when the context's value changes.