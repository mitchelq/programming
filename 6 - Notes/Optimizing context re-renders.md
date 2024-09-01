
You only need to optimize your context provider if all of these apply:
- The state in the context needs to change all the time
- The context has many consumers
- The app is actually slow / laggy


### options to optimize your context

- Pass components as children
[[Performance Optimization - Passing elements as children or regular props]]
- Memo all components that cannot be passed as children
- use useMemo for the provider value to prevent re-render of all consumers when updating a parent component of the Context provider
- Make sure to split context into multiple files for each type of context. Avoid context that depends on many different state.