# Code Standardization with Eslint and Prettier

## Introduction

Code standardization is crucial for maintaining consistency among individuals within a team, improving readability, and reducing errors. In this article, we will explore code standardization using ESLint for our Next.js (JavaScript) project to achieve good code standardization.

## Developer Software

To ensure a consistent development environment, we recommend the following software:

- **Visual Studio Code** or **Cursor** (based on VSCode but with AI). Choose one of them.
- **ESLint** (VSCode extension - optional, make sure developers get warnings or errors from the text editor directly).
- **Prettier** (VSCode extension - mandatory).

## Setup Project

To get started with ESLint in a Next.js project, we need to install ESLint, Prettier, and some additional plugins as devDependencies. Here is the list:

- `eslint^8` (latest version of v8, prevent install v8 higher) - ignore this if already installed when initiating the Next.js project.
- `prettier^3` (to make sure developers use the same Prettier version).
- `prettier-plugin-tailwindcss` (Prettier plugin for Tailwind CSS auto format, sync to ESLint also).
- `eslint-config-next` (provides a set of recommended rules and configurations from Next.js).
- `eslint-config-prettier` (sync ESLint & Prettier config).
- `eslint-plugin-prettier` (sync ESLint & Prettier plugin).
- `eslint-plugin-tailwindcss` (provides a set of recommended rules and configurations from Tailwind CSS).
- `eslint-plugin-jsx-a11y` (provides a set of recommended accessibility rules).

To install these dependencies, run the following command:

```bash
npm install eslint^8 prettier^3 prettier-plugin-tailwindcss eslint-config-next eslint-config-prettier eslint-plugin-prettier eslint-plugin-tailwindcss eslint-plugin-jsx-a11y --save-dev
```

## ESLint Configuration

Here's our ESLint configuration (will always be updated for any feedback and improvements):

```json
{
  "extends": [
    "next/core-web-vitals",
    "prettier",
    "plugin:jsx-a11y/recommended",
    "plugin:prettier/recommended",
    "plugin:tailwindcss/recommended",
    "plugin:eslint-plugin-prettier/recommended"
  ],
  "plugins": ["react", "prettier", "tailwindcss", "jsx-a11y"],
  "ignorePatterns": [
    "node_modules/",
    ".next/",
    "!.prettierrc.json",
    "!.eslintrc.json",
    "**/*.config.js"
  ],
  "rules": {
    "import/order": [
      "error",
      {
        "groups": [
          "builtin",
          "external",
          "internal",
          ["parent", "sibling", "index"],
          "object"
        ],
        "pathGroups": [
          {
            "pattern": "@/**/*",
            "group": "internal",
            "position": "before"
          }
        ],
        "pathGroupsExcludedImportTypes": ["builtin"],
        "alphabetize": {
          "order": "asc"
        },
        "newlines-between": "always"
      }
    ],
    "react/function-component-definition": [
      "warn",
      {
        "namedComponents": "arrow-function",
        "unnamedComponents": "arrow-function"
      }
    ],
    "react/jsx-pascal-case": "error",
    "camelcase": ["error", { "properties": "never" }],
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "off",
    "prettier/prettier": ["error", {}, { "usePrettierrc": true }],
    "@next/next/no-img-element": "off",
    "tailwindcss/classnames-order": "off",
    "tailwindcss/no-custom-classname": "off",
    "tailwindcss/no-contradicting-classname": "error",
    "react/no-unescaped-entities": "off",
    "no-unused-vars": "error",
    "@typescript-eslint/no-unused-vars": [
      "error",
      {
        "argsIgnorePattern": "^_",
        "varsIgnorePattern": "^_"
      }
    ],
    "@typescript-eslint/no-explicit-any": "error"
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "root": true
}
```

## ESLint Configuration Breakdown

### Extends

The `extends` property allows you to use predefined ESLint configurations. This helps in quickly setting up a base configuration that adheres to best practices.

```json
"extends": [
  "next/core-web-vitals",
  "prettier",
  "plugin:jsx-a11y/recommended",
  "plugin:prettier/recommended",
  "plugin:tailwindcss/recommended",
  "plugin:eslint-plugin-prettier/recommended"
]
```

- **`next/core-web-vitals`**: Enforces best practices and performance improvements specific to Next.js.
- **`prettier`**: Integrates Prettier to handle code formatting rules.
- **`plugin:jsx-a11y/recommended`**: Applies recommended accessibility rules.
- **`plugin:prettier/recommended`**: Applies recommended Prettier settings to ESLint.
- **`plugin:tailwindcss/recommended`**: Applies recommended Tailwind CSS linting rules.
- **`plugin:eslint-plugin-prettier/recommended`**: Treats Prettier rules as ESLint rules, ensuring consistent formatting.

### Plugins

The `plugins` property specifies additional ESLint plugins that add extra rules and capabilities.

```json
"plugins": ["react", "prettier", "tailwindcss", "jsx-a11y"]
```

- **`react`**: Adds React-specific linting rules.
- **`prettier`**: Integrates Prettier's formatting rules into ESLint.
- **`tailwindcss`**: Adds Tailwind CSS-specific linting rules.
- **`jsx-a11y`**: Adds accessibility-specific linting rules.

### Ignore Patterns

The `ignorePatterns` property specifies files and directories to be ignored by ESLint.

```json
"ignorePatterns": [
  "node_modules/",
  ".next/",
  "!.prettierrc.js",
  "!.eslintrc.js",
  "**/*.config.js"
]
```

- **`node_modules/`**: Ignores dependencies.
- **`.next/`**: Ignores Next.js build output.
- **`!.prettierrc.js`, `!.eslintrc.js`**: Ensures these configuration files are not ignored.
- **`**/\*.config.js`**: Ignores all configuration files with the `.config.js` extension.

### Rules

The `rules` property defines custom linting rules to enforce specific coding standards.

```json
"rules": {
  "import/order": [
    "error",
    {
      "groups": [
        "builtin",
        "external",
        "internal",
        ["parent", "sibling", "index"],
        "object"
      ],
      "pathGroups": [
        {
          "pattern": "@/**/*",
          "group": "internal",
          "position": "before"
        }
      ],
      "pathGroupsExcludedImportTypes": ["builtin"],
      "alphabetize": {
        "order": "asc"
      },
      "newlines-between": "always"
    }
  ],
  "react/function-component-definition": [
    "warn",
    {
      "namedComponents": "arrow-function",
      "unnamedComponents": "arrow-function"
    }
  ],
  "react/jsx-pascal-case": "error",
  "camelcase": ["error", { "properties": "never" }],
  "react-hooks/rules-of-hooks": "error",
  "react-hooks/exhaustive-deps": "off",
  "prettier/prettier": ["error", {}, { "usePrettierrc": true }],
    "@next/next/no-img-element": "off",
    "tailwindcss/classnames-order": "off",
    "tailwindcss/no-custom-classname": "off",
    "tailwindcss/no-contradicting-classname": "error",
    "react/no-unescaped-entities": "off",
    "no-unused-vars": "error",
    "@typescript-eslint/no-unused-vars": [
      "error",
      {
        "argsIgnorePattern": "^_",
        "varsIgnorePattern": "^_"
      }
    ],
    "@typescript-eslint/no-explicit-any": "error"
  }
}
```

#### `import/order`

This rule enforces a specific order for import statements to improve readability. As long as you've installed Prettier and enabled format on save, this rule can be automatically corrected by Prettier itself. If not, you can manually run `npm run prettier --write`.

- **Incorrect Code:**

  ```javascript
  import React, { useState } from "react"; // external
  import path from "path"; // builtin
  import customHook from "@/hooks/customHook"; // internal
  import { myFunction } from "../utils"; // parent
  import "./styles.css"; // sibling
  import { anotherFunction } from "./helpers"; // sibling
  import { myObject } from "./"; // index
  ```

- **Correct Code:**

  ```javascript
  import path from "path"; // builtin

  import React, { useState } from "react"; // external

  import customHook from "@/hooks/customHook"; // internal

  import { myFunction } from "../utils"; // parent

  import "./styles.css"; // sibling
  import { anotherFunction } from "./helpers"; // sibling

  import { myObject } from "./"; // index
  ```

#### `react/function-component-definition`

This rule warns if function components are not defined as arrow functions.

- **Incorrect Code:**

  ```javascript
  function MyComponent() {
    return <div>Hello World</div>;
  }
  ```

- **Correct Code:**
  ```javascript
  const MyComponent = () => {
    return <div>Hello World</div>;
  };
  ```

#### `react/jsx-pascal-case`

This rule enforces PascalCase for user-defined JSX components.

- **Incorrect Code:**

  ```javascript
  const myComponent = () => {
    return <div>Hello World</div>;
  };
  ```

- **Correct Code:**
  ```javascript
  const MyComponent = () => {
    return <div>Hello World</div>;
  };
  ```

#### `camelcase`

This rule enforces camelCase naming convention for variables and functions.

- **Incorrect Code:**

  ```javascript
  const my_variable = 10;
  ```

- **Correct Code:**
  ```javascript
  const myVariable = 10;
  ```

#### `react-hooks/rules-of-hooks`

This rule enforces the rules of React Hooks.

- **Incorrect Code:**

  ```javascript
  function MyComponent() {
    if (true) {
      const [state, setState] = useState(0);
    }
    return <div>Hello World</div>;
  }
  ```

- **Correct Code:**
  ```javascript
  function MyComponent() {
    const [state, setState] = useState(0);
    return <div>Hello World</div>;
  }
  ```

#### `react-hooks/exhaustive-deps`

This rule is turned off to allow more flexibility in managing dependencies in React Hooks.

#### `prettier/prettier`

This rule enforces Prettier formatting rules.

- **Incorrect Code:**

  ```javascript
  const foo = { bar: [1, 2, 3] };
  ```

- **Correct Code:**
  ```javascript
  const foo = { bar: [1, 2, 3] };
  ```

#### `@next/next/no-img-element`

This rule is turned off to allow the use of the `<img>` element instead of Next.js's `<Image />` component.

#### `tailwindcss/classnames-order`

This rule is turned off to prevent conflicts with Prettier's Tailwind CSS class name order.

#### `tailwindcss/no-custom-classname`

This rule is turned off to give flexibility for using third-party custom class names.

#### `tailwindcss/no-contradicting-classname`

This rule enforces that there are no contradicting class names in Tailwind CSS.

- **Incorrect Code:**

  ```javascript
  <div className="bg-blue-500 bg-red-500">Hello World</div>
  ```

- **Correct Code:**
  ```javascript
  <div className="bg-blue-500">Hello World</div>
  ```

#### `react/no-unescaped-entities`

This rule is turned off to allow unescaped entities in JSX.

#### `no-unused-vars`

This rule enforces that there are no unused variables in the code.

- **Incorrect Code:**

  ```javascript
  const unusedVariable = 42;
  const MyComponent = () => {
    return <div>Hello World</div>;
  };
  ```

- **Correct Code:**
  ```javascript
  const MyComponent = () => {
    return <div>Hello World</div>;
  };
  ```

#### `@typescript-eslint/no-unused-vars`

This rule detects and reports on variables that are declared but never used in your TypeScript code.

```json
"@typescript-eslint/no-unused-vars": [
  "error",
  {
    "argsIgnorePattern": "^_",
    "varsIgnorePattern": "^_"
  }
]
```

- **`"error"`**: This setting will throw an error if unused variables are detected.
- **`argsIgnorePattern`**: This option specifies a pattern for function arguments that should be ignored by this rule. In this case, any argument starting with an underscore (`_`) will be ignored.
- **`varsIgnorePattern`**: Similar to `argsIgnorePattern`, but for variables. Any variable starting with an underscore will be ignored.

This configuration is useful when you want to declare variables or function parameters that you don't intend to use, but want to keep for clarity or future use. By prefixing them with an underscore, you're telling ESLint to ignore them.

- **Incorrect Code:**

  ```typescript
  function exampleFunction(unusedParam: string, usedParam: number) {
    console.log(usedParam);
  }

  const unusedVariable = 5;
  ```

- **Correct Code:**

  ```typescript
  function exampleFunction(_unusedParam: string, usedParam: number) {
    console.log(usedParam);
  }

  const _unusedVariable = 5;
  ```

#### `@typescript-eslint/no-explicit-any`

This rule disallows the use of the `any` type in TypeScript.

```json
"@typescript-eslint/no-explicit-any": "error"
```

The `any` type in TypeScript essentially turns off type checking for the variable it's applied to, which can lead to type-related bugs. This rule encourages you to use more specific types, improving type safety in your code.

- **Incorrect Code:**

  ```typescript
  function example(param: any) {
    console.log(param);
  }

  const value: any = "string";
  ```

- **Correct Code:**

  ```typescript
  function example(param: unknown) {
    console.log(param);
  }

  const value: string = "string";
  ```

These rules together encourage more type-safe and cleaner TypeScript code, reducing potential bugs and improving code quality.

### Settings

The `settings` property provides additional configuration for specific plugins.

```json
"settings": {
  "react": {
    "version": "detect"
  }
}
```

- **`react.version`**: Automatically detects the React version to use.

### Root

The `root` property indicates that this is the root ESLint configuration file, preventing ESLint from looking for configurations in parent directories.

```json
"root": true
```

# Prettier Configuration

```json
{
  "plugins": ["prettier-plugin-tailwindcss"],
  "semi": true,
  "singleQuote": false,
  "trailingComma": "all",
  "printWidth": 80,
  "tabWidth": 2,
  "endOfLine": "auto",
  "proseWrap": "always"
}
```

## Configuration Breakdown

### `plugins`

```json
"plugins": ["prettier-plugin-tailwindcss"]
```

- **Description**: This specifies additional plugins to be used by Prettier. In this case, `prettier-plugin-tailwindcss` is included to automatically sort Tailwind CSS classes in your code.
- **Example**:

  ```html
  <!-- Before -->
  <div class="text-center bg-red-500 p-4"></div>

  <!-- After (sorted by plugin) -->
  <div class="bg-red-500 p-4 text-center"></div>
  ```

### `semi`

```json
"semi": true
```

- **Description**: This setting enforces the use of semicolons at the end of statements.
- **Example**:

  ```javascript
  // Before
  const foo = "bar";

  // After
  const foo = "bar";
  ```

### `singleQuote`

```json
"singleQuote": false
```

- **Description**: This setting enforces the use of double quotes for strings instead of single quotes.
- **Example**:

  ```javascript
  // Before
  const foo = "bar";

  // After
  const foo = "bar";
  ```

### `trailingComma`

```json
"trailingComma": "all"
```

- **Description**: This setting enforces the use of trailing commas wherever possible, such as in objects, arrays, and function parameters.
- **Example**:

  ```javascript
  // Before
  const obj = {
    foo: "bar",
    baz: "qux",
  };

  // After
  const obj = {
    foo: "bar",
    baz: "qux",
  };
  ```

### `printWidth`

```json
"printWidth": 80
```

- **Description**: This setting specifies the maximum line length that Prettier will wrap on. Lines longer than 80 characters will be wrapped.
- **Example**:

  ```javascript
  // Before
  const longString =
    "This is a very long string that will be wrapped by Prettier because it exceeds the print width of 80 characters.";

  // After
  const longString =
    "This is a very long string that will be wrapped by Prettier because it exceeds the print width of 80 characters.";
  ```

### `tabWidth`

```json
"tabWidth": 2
```

- **Description**: This setting specifies the number of spaces per indentation level.
- **Example**:

  ```javascript
  // Before
  function foo() {
    console.log("bar");
  }

  // After
  function foo() {
    console.log("bar");
  }
  ```

### `endOfLine`

```json
"endOfLine": "auto"
```

- **Description**: This setting maintains existing end-of-line characters (LF or CRLF) in the file. It helps to avoid issues with different operating systems.
- **Example**:

  ```javascript
  // Before (on Windows)
  const foo = "bar"; // CRLF

  // After (on Unix-based OS)
  const foo = "bar"; // LF
  ```

### `proseWrap`

```json
"proseWrap": "always"
```

- **Description**: This setting ensures that markdown text is always wrapped according to the `printWidth` setting.
- **Example**:

  ```markdown
  <!-- Before -->

  This is a very long line in a markdown file that will be wrapped by Prettier because it exceeds the print width of 80 characters.

  <!-- After -->

  This is a very long line in a markdown file that will be wrapped by Prettier
  because it exceeds the print width of 80 characters.
  ```

### Additional Tips

1. **Automate Linting**: Integrate ESLint into your CI/CD pipeline to automatically lint code on every push or pull request. This ensures that code quality is maintained across the team.
2. **Editor Configuration**: Ensure all team members have their editors configured to use ESLint and Prettier. This can be done by sharing editor configuration files like `.vscode/settings.json`.

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll": "always"
  },
  "eslint.validate": ["javascript", "javascriptreact"],
  "prettier.requireConfig": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

Disclaimer: This documentation was written with the assistance of AI.
