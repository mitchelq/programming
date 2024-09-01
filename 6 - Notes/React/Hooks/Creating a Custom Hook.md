#### Created: 2024-08-21
#### Tags: [[React]] [[React Hooks]]
# Creating a Custom Hook

## Guidelines:
1. Start the hook name with "use" (e.g., useFetch, useForm)
2. Ensure the hook has a single responsibility
3. Use other hooks inside your custom hook
4. Return any values that components using this hook might need

## Example:
```javascript
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch(url);
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    }
    fetchData();
  }, [url]);

  return { data, loading, error };
}
```

## When to use:
- When you have component logic that can be reused across multiple components
- When you want to share stateful logic between components without changing their structure