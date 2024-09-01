#### Created: 2024-08-22
#### Tags: [[React]] [[CSS]] [[Styling]]
# Styling options in React

React doesn't care about styling. Here are the various options available:

| Styling Option                     | Where?                          | How?                  | Scope               | Based On   |
| ---------------------------------- | ------------------------------- | --------------------- | ------------------- | ---------- |
| Inline CSS                         | JSX elements                    | style prop            | JSX element (Local) | CSS        |
| CSS or Sass file                   | External file                   | className prop        | Entire app          | CSS        |
| [[CSS Modules]]                    | One external file per component | className prop        | Component           | CSS        |
| CSS-in-JS                          | External file or component file | Creates new component | Component           | JavaScript |
| Utility-first CSS (e.g., Tailwind) | JSX elements                    | className prop        | JSX element         | CSS        |

## Pros and Cons of Each Option

1. Inline CSS
   Pros:
   - Quick and easy for small, one-off styles
   - Styles are scoped to the element
   - No need for additional files

   Cons:
   - Can make JSX messy and hard to read
   - No access to CSS features like media queries
   - Difficult to maintain for larger applications

2. CSS or Sass file
   Pros:
   - Familiar syntax for most developers
   - Can use all CSS features
   - Easy to create global styles

   Cons:
   - Global scope can lead to naming conflicts
   - Can become difficult to manage in large applications
   - Requires careful organization to avoid specificity issues

3. [[CSS Modules]]
   Pros:
   - Scoped to component, avoiding naming conflicts
   - Can use all CSS features
   - Keeps styles separate from component logic

   Cons:
   - Requires additional setup
   - Can be overkill for small projects
   - May require additional tooling for some features (e.g., composition)

4. CSS-in-JS
   Pros:
   - Full power of JavaScript for styling
   - Scoped to component
   - Can create dynamic styles easily

   Cons:
   - Steeper learning curve
   - Can increase bundle size
   - May have performance overhead

5. Utility-first CSS (e.g., Tailwind)
   Pros:
   - Rapid development with pre-defined utility classes
   - Consistent design system
   - Small file sizes when properly configured

   Cons:
   - HTML can become cluttered with many classes
   - Learning curve for the utility class names
   - Can be less flexible for custom designs

## Alternative to styling with CSS
UI libraries like MUI, Chakra UI, Mantine, etc., provide pre-styled components and theming capabilities.

Pros:
- Rapid development with pre-built components
- Consistent design out of the box
- Often include accessibility features

Cons:
- Can lead to similar-looking applications
- Customization can be challenging
- May increase bundle size significantly