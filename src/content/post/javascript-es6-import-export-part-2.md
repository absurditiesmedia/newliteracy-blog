---
publishDate: "24 Oct 2024"
title: Part 2, Understanding Named and Default Exports
description: Where and why to use default and named exports in ES6
excerpt: Both named and default exports allow you to share functionality between modules, but there are key differences in how they work and when you should use each.
tags: ["NodeJS","JavaScript", "ECMAScript 2015"]
coverImage:
    src: "../../assets/jses6_logo.png"
    alt: "vscode logo"
---

## Introduction

In the previous part, we introduced the basics of **importing** and **exporting** in JavaScript ES6, covering both **named** and **default** exports. Now, it’s time to explore these two types of exports more deeply.

Both named and default exports allow you to share functionality between modules, but there are key differences in how they work and when you should use each. This part will explain those differences, highlight common use cases, and offer guidance on best practices for using named and default exports effectively.

---

## Named Exports: The Power of Multiple Exports

**Named exports** allow you to export multiple items from a module. Whether it's functions, constants, or objects, named exports make it easy to share multiple pieces of functionality from a single file.

### Key Features of Named Exports:
1. **Multiple Exports Per Module**: You can export as many items as you need from a single module. This is ideal for utility libraries or modules that provide various functions.

2. **Must Be Imported by Exact Name**: When importing, you need to know the exact name of the item. This ensures clarity and reduces confusion in large projects, but it also means more precision is required from the developer.

3. **Export Throughout the Module**: Named exports can be spread throughout the module or collected in a single `export` statement at the end.

### Example of Named Exports:
```javascript
// mathUtils.js
export const pi = 3.14159;
export function square(x) {
  return x * x;
}
export function cube(x) {
  return x * x * x;
}
```

In the above example, we are exporting multiple values: a constant `pi`, and two functions `square` and `cube`. Any other module can now import one or all of these exports.

### Importing Named Exports:
To use the exports, you must explicitly import them by name:

```javascript
// app.js
import { pi, square, cube } from './mathUtils.js';

console.log(square(3));   // Output: 9
console.log(cube(2));     // Output: 8
console.log(pi);          // Output: 3.14159
```

You can choose to import only what you need:

```javascript
// app.js
import { square } from './mathUtils.js';

console.log(square(4));   // Output: 16
```

### Renaming Named Imports:
If you need to avoid name conflicts or improve clarity, you can **rename** a named export during import:

```javascript
import { square as squareNumber } from './mathUtils.js';

console.log(squareNumber(5));   // Output: 25
```

This allows you to adapt the import to fit the context of your code, while keeping the original export name in the module.

---

## Default Exports: The "One Main Thing" Approach

**Default exports** are used when a module only has one primary value to export. They simplify the import process because they don’t require you to know the export name — you can assign any name during the import.

### Key Features of Default Exports:
1. **One Default Export Per Module**: A module can have only **one** default export, which is meant to represent the main functionality or object the module provides.

2. **Can Be Imported with Any Name**: When you import a default export, you don’t need to know its original name. You can import it using any name you like, which simplifies the process, especially when integrating third-party libraries.

### Example of a Default Export:
```javascript
// calculator.js
export default function add(a, b) {
  return a + b;
}
```

In this example, `add` is exported as the default export. When importing, you can name it however you want:

```javascript
// app.js
import sum from './calculator.js';

console.log(sum(5, 3));  // Output: 8
```

Notice how we imported `add` as `sum` — this flexibility is one of the key advantages of default exports.

---

## Named vs Default Exports: When to Use Each?

Choosing between named and default exports often depends on how your module is structured and how you expect others to use it. Here’s a breakdown of when to use each:

### When to Use Named Exports:
1. **Multiple Exports**: If your module provides multiple utilities or pieces of functionality, named exports make the most sense. This is common in utility libraries, where each function or constant serves a distinct purpose.

2. **Clarity and Explicitness**: Named exports encourage clarity since you must explicitly state which parts of the module you are importing. This helps make the code easier to read and understand, especially in large projects.

3. **Granular Imports**: If users of your module might only need specific pieces of functionality (e.g., one or two functions), named exports allow them to import only what they need, keeping their code clean and efficient.

### When to Use Default Exports:
1. **Single Responsibility**: When your module is centered around a single concept, object, or function, a default export is ideal. It signals to the user that the module’s purpose is singular and straightforward.

2. **Ease of Import**: Default exports are easier to import, especially when the name of the export isn’t critical to the module’s purpose. This can make using your module more intuitive, as users don’t need to worry about remembering the exact name of the export.

3. **Library Integration**: If you are writing a library or framework, default exports can help make the API simpler. A single default export can represent the "main" object or function that the user interacts with.

---

## Mixing Named and Default Exports

In some cases, you may want to use both named and default exports in the same module. For example, you might have a primary function as the default export, but also provide additional named exports for utilities or constants:

```javascript
// shapes.js
export default function drawCircle(radius) {
  console.log('Drawing a circle with radius', radius);
}

export function drawSquare(sideLength) {
  console.log('Drawing a square with side length', sideLength);
}

export const pi = 3.14159;
```

When importing, you can bring in both the default export and any named exports you need:

```javascript
// app.js
import drawCircle, { drawSquare, pi } from './shapes.js';

drawCircle(10);      // Drawing a circle with radius 10
drawSquare(5);       // Drawing a square with side length 5
console.log(pi);     // 3.14159
```

This allows for flexibility, combining a module’s primary export with any secondary functionality.

---

## Best Practices for Exporting and Importing

To keep your codebase clean and efficient, here are some best practices for using named and default exports:

1. **Be Consistent**: Choose a consistent pattern for your module exports. If a module is focused on one main function or object, use a default export. If it provides multiple utilities, stick with named exports.

2. **Avoid Overusing Default Exports**: While default exports can make importing easier, they can also lead to ambiguity in large projects where many modules are imported. Prefer named exports when multiple parts of a module are equally important.

3. **Use Named Imports for Specificity**: When possible, prefer named imports for clarity and precision. This helps reduce confusion, especially in codebases with many dependencies.

4. **Limit Mixing of Export Types**: While it’s possible to mix default and named exports, avoid doing so unless it adds significant value. Mixing export types can make the module harder to understand and use.

---

## Conclusion

In **Part 2**, we’ve taken an in-depth look at **named** and **default exports**, comparing their use cases, advantages, and when to choose one over the other. By understanding the strengths and trade-offs of each export type, you can better organize your code and create modules that are easy to maintain and integrate.

In the next part, we’ll explore **re-exports and module aggregation**, which will help you streamline your imports and organize large projects more efficiently.


- *LAST:*[Part 1: Getting Started with Modules](/posts/javascript-es6-import-export-part-1)
- *NEXT:*[Part 3: Re-exports and Module Aggregation](/posts/javascript-es6-import-export-part-3)
