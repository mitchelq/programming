#### Created: 2024-09-01
#### Tags: [[React]] [[VS code extentions]] [[Snippets]] [[File Templates]]
#### Links: [[React Components]] [[Custom Hooks]] [[Styled Components]] [[CSS Modules]]

# React File Snippets for VS Code

## Overview
This note contains VS Code snippets for creating new React component files and other useful React-related snippets. These snippets will generate entire file contents or commonly used code blocks to speed up your React development process.

## When to Use
- When starting a new React component file
- When you need to quickly insert common React patterns or imports
- To ensure consistency in file structure and coding patterns across your React project

## Snippets

### 1. React Functional Component File
```json
"React Functional Component": {
  "prefix": "rfc",
  "scope": "javascript,typescript,javascriptreact",
  "body": [
    "function ${TM_FILENAME_BASE}() {",
    "\treturn (",
    "\t\t<div>",
    "\t\t\t$0",
    "\t\t</div>",
    "\t)",
    "}",
    "",
    "export default ${TM_FILENAME_BASE}",
    ""
  ],
  "description": "React component"
}
```

### 2. Console Log
```json
"Print to console": {
  "prefix": "cl",
  "scope": "javascript,typescript,javascriptreact",
  "body": ["console.log($1)"],
  "description": "console.log"
}
```

### 3. Import CSS Module
```json
"importCSSModule": {
  "prefix": "csm",
  "scope": "javascript,typescript,javascriptreact",
  "body": ["import styles from './${TM_FILENAME_BASE}.module.css'"],
  "description": "Import CSS Module as `styles`"
}
```

### 4. React Styled Component
```json
"reactStyledComponent": {
  "prefix": "rsc",
  "scope": "javascript,typescript,javascriptreact",
  "body": [
    "import styled from 'styled-components'",
    "",
    "const Styled${TM_FILENAME_BASE} = styled.$1``",
    "",
    "function ${TM_FILENAME_BASE}() {",
    "\treturn (",
    "\t\t<Styled${TM_FILENAME_BASE}>",
    "\t\t\t$0",
    "\t\t</Styled${TM_FILENAME_BASE}>",
    "\t)",
    "}",
    "",
    "export default ${TM_FILENAME_BASE}",
    ""
  ],
  "description": "React styled component"
}
```

## How to Add and Use These Snippets in VS Code

1. In VS Code, go to File > Preferences > User Snippets.
2. Choose "javascriptreact.json" (for .jsx files) or "typescriptreact.json" (for .tsx files).
3. Paste the snippets into the file.
4. Save the file.

To use these snippets:
- For file templates (rfc, rsc): Create a new file with a .jsx or .tsx extension, type the prefix, and press Tab.
- For in-file snippets (cl, csm): In an existing file, type the prefix and press Tab.

## Key Points
- File template snippets create entire file contents.
- In-file snippets insert commonly used code blocks.
- Component and file names will automatically match the file name where applicable.
- The cursor will be placed between the divs in the React Functional Component snippet.
- The console.log snippet provides a quick way to add debug statements.
- The CSS module import snippet automatically uses the current file name for the import.

## Best Practices
- Use meaningful file names as they will become your component names.
- Customize these templates to match your project's coding standards.
- Use the console.log snippet judiciously and remember to remove debug statements before committing code.

## Common Pitfalls
- Ensure you're using the correct file extension (.jsx or .tsx) when creating new files.
- Remember to add any necessary imports that aren't included in the snippets.
- When using styled-components, make sure you have the library installed in your project.

## Related Concepts
- [[React Components]]
- [[Styled Components]]
- [[CSS Modules]]
- [[VS Code Productivity Tips]]

## Additional Notes
You can further customize these snippets by adding more commonly used imports, context usage, or other patterns you frequently use in your components. Remember to adjust the scope of the snippets if you're working with TypeScript (.ts or .tsx files).