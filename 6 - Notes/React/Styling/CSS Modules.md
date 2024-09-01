#### Created: 2024-08-22
#### Tags: [[React]] [[Styling]] [[CSS]]
#### Links:
[[Styling options in React]]
# CSS Modules

How to implement:

Create a file for each component you want to style. naming convention: ComponentName.module.css

Then add styling to the file. Be sure to use classes and do not directly style an element as this will not be scoped.
```css
.nav {
  background-color: aqua;

  & ul {
    display: flex;
    justify-content: space-between;
    list-style: none;
  }

  :global(.active) {
    background-color: green;
  }
}
```

use it in your component:

```jsx
import { NavLink } from "react-router-dom";
import styles from "./PageNav.module.css";

function PageNav() {
  return (
    <nav className={styles.nav}>
      <ul>
        <li>
          <NavLink to="/">Home</NavLink>
        </li>
        ...more
      </ul>
    </nav>
  );
}

export default PageNav;
```


IMPORTANT:
When using CSS modules, react adds a suffix identifier to the classnames specified. So if you want to style a class that is added in a dynamic way, for example "active" on NavLinks, you can't style it like this:
```css
.nav .active {
	background-color: green;
}
```
This won't work because this class will get a suffix and look like this `.active_ssfha_1` and will not match the classname `.active` Instead, you will need to set it as a global class, like this:
```css
.nav :global(.active) {
	background-color: green;
}
```