#### Created: 2024-08-21
#### Tags: [[React]]
# Creating a Regular Function

Regular functions in React are used for logic that doesn't involve hooks or component lifecycle.

## Guidelines:
1. Keep the function pure when possible (same input always produces the same output)
2. Name the function descriptively based on its purpose
3. Use parameters to make the function flexible and reusable
4. Place the function outside of your component if it doesn't rely on props or state

## Example:
```javascript
function formatCurrency(amount, currency = 'USD') {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: currency,
  }).format(amount);
}
```

## When to use:
- For utility functions that don't depend on React's lifecycle or hooks
- When you need to perform calculations or transformations that don't require state or side effects
- For code that you want to reuse across different parts of your application, including non-React parts