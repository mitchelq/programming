#### Created: 2024-08-23
#### Tags: [[React]] [[React Router]]
# Programmatic Navigation (useNavigate)


To navigate programmatic to a URL using the useNavigate hook provided by React Router simply use this:

```jsx
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();

<button
    onClick={() => {
	    navigate("form");
    }}
>
    navigate to form
</button>
``` 

We can also use the navigate hook to move back:

```jsx
<button
    onClick={(e) => {
	    e.preventDefault();
	    navigate(-1);
    }}
>
    &larr; Back
</button>
```

We can specify how many steps back (or forward), but -1 is the most used option.
