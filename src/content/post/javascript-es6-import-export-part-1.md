---
publishDate: "24 Oct 2024"
title: Part 1, Getting Started with Modules
description: The fundamental concepts of importing and exporting in ES6
excerpt: Before ES6, JavaScript did not have a native module system, which made it difficult to split large codebases into manageable pieces
tags: ["NodeJS","JavaScript", "ECMAScript 2015"]
coverImage:
    src: "../../assets/jses6_logo.png"
    alt: "vscode logo"
---

## Introduction

Before ES6, JavaScript did not have a native module system, which made it difficult to split large codebases into manageable pieces. Developers relied on patterns like the Module Pattern, or third-party libraries such as RequireJS or CommonJS, to organize code into reusable components. However, with ES6, JavaScript introduced native module support, giving developers a clean and efficient way to manage dependencies and organize code.

In this section, we’ll start with the fundamental concepts of **importing** and **exporting** in ES6, laying the foundation for more advanced topics later on.


### What is a Module?

A **module** in JavaScript is simply a file containing reusable code. Each module can define variables, functions, objects, or classes and expose them to other modules using the `export` statement. Modules also keep code isolated, meaning variables and functions declared inside a module are not accessible to the global scope, unless explicitly exported.

For example, imagine you have a file `math.js` where you define a function to add two numbers:

```javascript
// math.js
export function add(a, b) {
  return a + b;
}
```

The function `add` is now available for other modules to use, but only if they explicitly import it.

---

### Basic `export` Syntax

There are two main ways to export from a module in ES6: **named exports** and **default exports**. In this part, we'll focus on named exports.

#### Named Exports

A named export allows you to export multiple variables or functions from a module. Each item must be explicitly named in both the export and the corresponding import. Here's how it works:

```javascript
// utilities.js
export const pi = 3.14159;
export function multiply(x, y) {
  return x * y;
}
```

You can export as many items as needed from the module. When importing them into another file, you specify the exact names of the exports you want to use:

```javascript
// app.js
import { pi, multiply } from './utilities.js';

console.log(multiply(pi, 2)); // Output: 6.28318
```

In this example, `pi` and `multiply` were exported from `utilities.js` and then imported into `app.js`. You must use the same names when importing named exports.

---

### Basic `import` Syntax

The `import` statement is used to bring in variables, functions, objects, or classes from another module. As seen above, you use curly braces `{}` to specify named exports:

```javascript
import { export1, export2 } from 'module';
```

You can also rename imported items using the `as` keyword, which can be useful if there are naming conflicts or if you want to give them more meaningful names:

```javascript
import { multiply as mult } from './utilities.js';

console.log(mult(5, 6)); // Output: 30
```

---

### Default Exports

Sometimes, you may want to export a single value as the default export. A **default export** is useful when a module only provides one main functionality or object, making it easier to import without specifying a name. Here's how it works:

```javascript
// math.js
export default function subtract(a, b) {
  return a - b;
}
```

You can import a default export without using curly braces:

```javascript
// app.js
import subtract from './math.js';

console.log(subtract(10, 5)); // Output: 5
```

Default exports are common for modules where there is one primary function or object. They help make your imports cleaner and reduce boilerplate.

---

### Combining Named and Default Exports

It is possible for a module to use both named and default exports. For example:

```javascript
// math.js
export const pi = 3.14159;
export default function add(a, b) {
  return a + b;
}
```

You can import both like this:

```javascript
// app.js
import add, { pi } from './math.js';

console.log(add(pi, 2)); // Output: 5.14159
```

In this case, `add` is the default export, and `pi` is a named export.

---

### Exporting As You Declare

You can also export variables or functions as you declare them, without repeating the `export` keyword:

```javascript
export const name = 'John';
export function greet() {
  console.log('Hello, ' + name);
}
```

Or combine everything into a single export at the end of the file:

```javascript
const name = 'John';
function greet() {
  console.log('Hello, ' + name);
}

export { name, greet };
```

---

### Importing Entire Modules

In some cases, you may want to import everything from a module under a single namespace. This is useful for larger modules with many exports:

```javascript
// utilities.js
export const pi = 3.14159;
export function multiply(x, y) {
  return x * y;
}
export function divide(x, y) {
  return x / y;
}
```

Instead of importing each export individually, you can import the whole module under an alias:

```javascript
// app.js
import * as utils from './utilities.js';

console.log(utils.multiply(3, 4));  // Output: 12
console.log(utils.pi);              // Output: 3.14159
```

Here, the entire module is imported as the `utils` object, and you can access each export as a property of that object.

---

### Recap

In **Part 1**, we’ve covered:

- What modules are and why they are important.
- The basic syntax for exporting and importing in JavaScript ES6.
- Named exports, default exports, and how to import them.
- Combining named and default exports.
- Importing an entire module under an alias.

In the next part, we’ll delve deeper into the differences between **named and default exports**, including best practices for choosing between them and more detailed examples to solidify your understanding.

- *LAST:*[Introduction](/posts/javascript-es6-import-export-introduction)
- *NEXT:*[Part 2, Understanding Named and Default Exports](/posts/javascript-es6-import-export-part-3)
