# Differences Between `useContext()`, Redux, and `useReducer()`

| Feature            | `useContext()`                     | `useReducer()`                     | Redux                            |
|--------------------|----------------------------------|-----------------------------------|----------------------------------|
| **Purpose**       | Provides access to a React Context for state sharing. | Manages local component state with a reducer function. | Manages global application state in a centralized store. |
| **Scope**         | Context API for prop drilling avoidance. | Component-level state management. | Global state management across the app. |
| **Complexity**    | Low – just a wrapper around Context API. | Moderate – needs a reducer function. | High – requires setup with actions, reducers, and middleware. |
| **State Structure** | Simple key-value store. | Usually limited to component-level state. | Highly structured state with reducers and actions. |
| **Performance**   | Can cause unnecessary re-renders if not optimized. | Efficient for component-level state. | Optimized with selectors, memoization, and middleware like Redux Toolkit. |
| **Middleware**    | No built-in support. | No built-in support. | Supports middleware (e.g., Redux Thunk, Saga). |
| **Async Handling** | Needs external state management (e.g., useReducer with useEffect). | Needs side-effects handled separately (e.g., useEffect). | Supports async actions via middleware. |
| **Best For**      | Passing down simple state like themes or auth status. | Component-level state that is complex but does not need global access. | Large-scale applications with shared, structured state. |
| **Example Usage** | `<ThemeContext.Provider value={theme}>` | `const [state, dispatch] = useReducer(reducer, initialState);` | `store.dispatch({ type: 'ACTION_TYPE' })` |

---

## When to Use Each:
- **`useContext()`** → Best for sharing simple state like themes, authentication, or user preferences.
- **`useReducer()`** → Best for component-local state that involves complex logic, such as forms or state machines.
- **Redux** → Best for large applications where state needs to be managed globally across multiple components.

### 🚀 TL;DR:
- Use **`useContext()`** for *prop drilling avoidance*.
- Use **`useReducer()`** for *component state with complex logic*.
- Use **Redux** for *scalable global state management*.

