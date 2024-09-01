#### Created: 2024-08-23
#### Tags: [[React]] [[URL]] [[React Router]]
# URL for State Management

Using the URL to store UI state and as an alternative to useState is an excellent solution in some situations. For example: open/closed panels, currently selected list items, list sorting order, applied list filters.

1. Easy way to store state in a **global place**, accessible to **all components** in the app
2. Good way to **"pass" data** from one page into the next page
3. Makes it possible to **bookmark and share** the page with the exact UI state it had at the time

## Path

`www.example.com`<span style="border: 2px solid red; font-weight: bold; padding: 2px 2px;">/app/cities/</span>`lisbon?lat=38.728&lng=-9.141`




## Params

`www.example.com/app/cities/`<span style="border: 2px solid green; font-weight: bold; padding: 2px 2px;">lisbon</span>`?lat=38.728&lng=-9.141`

### Usage

define the param in the Route. Don't nest the route
```jsx
<Route
    path="cities"
    element={<CityList cities={cities} isLoading={isLoading} />}
/>
<Route path="cities/:cityId" element={<City />} />
```

To create a link to the route:
```jsx
const id = "abc123"

<Link className={styles.cityItem} to={`${id}`}></Link>
```

**NOTE**: using a "/" before the id will get the path from the root, so: www.example.com/abc123. If not using the "/" the route will be added to the current path, which could be /app/cities/

Retrieving the param in a component:

```jsx
import { useParams } from "react-router-dom";

const params = useParams(); // params = {cityId: 'abc123'}
```
## Query string

`www.example.com/app/cities/lisbon?`<span style="border: 2px solid blue; font-weight: bold; padding: 2px 2px;">lat=38.728&lng=-9.141</span>

### Usage

For the querystring we don't have to define it in the actual route, just add it to the link we are calling:
```jsx
<Link
    className={styles.cityItem}
    to={`${id}?lat=${position.lat}&lng=${position.lng}`}
>
```

To retrieve it in a component:
```jsx
import { useSearchParams } from "react-router-dom";

const [searchParams, setSearchParams] = useSearchParams();
const lat = searchParams.get("lat");
const lng = searchParams.get("lng");

console.log(lat, lng);
```

And we can use the setSearchParams function to update the querystring:
```jsx
<button
    onClick={() => {
	    setSearchParams({ lat: 40.242, lng: 50.113 });
	    }}
>
    Change params
</button>
```

