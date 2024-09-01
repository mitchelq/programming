#### Created: 2024-08-26
#### Tags:
# Protected Route


```jsx
function ProtectedRoute({ children }) {
	const { isAuth } = useAuth();

	return isAuth ? children : <Navigate to="/" />;
}
```




