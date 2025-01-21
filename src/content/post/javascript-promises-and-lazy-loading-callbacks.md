---
publishDate: "24 October 2024"
title:  "Understanding JavaScript Promises and Lazy Loading Callbacks"
description: "One of the advantages of ES6 Promises is the ability to lazy load callback functions."
excerpt: "A key feature of ES6 Promises is that they don't immediately execute the callback functions passed to the `then` method. Instead, the callback is only queued to execute once the promise resolves or rejects."
tags: ["JavaScript", "ECMAScript 2015", "lazy-loading", "asynchronous"]
coverImage:
    src: "../../assets/jses6_logo.png"
    alt: "JavaScript ES6 Logo"

---

In JavaScript, **thenables** play a key role in asynchronous programming, particularly with Promises in ES6. One of the advantages of ES6 Promises (which use thenables) over older implementations like jQuery’s deferred objects is the ability to **lazy load callback functions**.

## Thenables in ES6

As mentioned earlier, a *thenable* is any object that has a `then` method, making it "promise-like." ES6 Promises, introduced in ECMAScript 2015 (ES6), are a formalization of the thenable concept and provide a built-in way to manage asynchronous operations. They have precise rules for managing asynchronous code, including **lazy evaluation** of callbacks.

A key feature of ES6 Promises is that they don't immediately execute the callback functions passed to the `then` method. Instead, the callback is only queued to execute once the promise resolves or rejects. This is referred to as **lazy loading** the callback functions.

Here’s how that works in practice:

```javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('ES6 Promise resolved!'), 1000);
});

myPromise.then(result => {
  console.log(result);  // Outputs "ES6 Promise resolved!" after 1 second
});
```

In this example, the `then` method does not execute immediately. Instead, it waits until the promise is resolved (after 1 second) before running the callback function.

## Lazy Loading Callbacks in ES6 Promises

The concept of **lazy loading** in ES6 Promises is an important shift from earlier asynchronous implementations. The idea is that the promise itself can start immediately (when the executor function is invoked), but the callback functions passed into `then()` or `catch()` are only triggered when the promise resolves or rejects.

This means that the code passed into `then()` is not run until absolutely necessary, allowing efficient management of asynchronous flows and preventing unnecessary execution of code.

For example:

```javascript
const promise = new Promise((resolve, reject) => {
  console.log("Promise started");
  setTimeout(() => resolve('Done'), 2000);
});

promise.then(() => console.log("This runs when resolved"));  // Lazy-loaded
console.log("Code after promise");
```

This outputs:
```
Promise started
Code after promise
This runs when resolved  // after 2 seconds
```

Here, the callback inside `then()` is not executed immediately but is "lazy-loaded" — it waits for the promise to resolve before running. The asynchronous operation (the `setTimeout`) is initiated immediately, but the code passed into `then()` doesn't run until the result is available. This lazy loading improves both clarity and efficiency when managing async tasks.

## jQuery Deferred Objects vs ES6 Thenables

Before ES6, libraries like **jQuery** implemented their own versions of thenables via **Deferred objects**. While jQuery's Deferred objects offered a way to handle asynchronous actions and chaining, there was no built-in mechanism for lazy loading the callbacks. This meant that callbacks could sometimes be eagerly evaluated or executed immediately based on how the asynchronous chain was set up.

Consider this example with jQuery Deferred:

```javascript
const deferred = $.Deferred();

deferred.done(() => console.log('jQuery Deferred resolved'));
deferred.resolve();
```

Unlike ES6 Promises, jQuery’s `.done()` method executes the callback immediately if the deferred object is already resolved when the callback is added. This can lead to situations where callbacks are executed unexpectedly as soon as they're attached, making it harder to reason about the exact timing of execution.

In contrast, ES6 Promises don’t exhibit this behavior. Even if a promise is already resolved, the callback passed to `then()` will always be added to the job queue and run asynchronously after the current JavaScript execution cycle, ensuring **consistent and predictable execution**:

```javascript
const promise = Promise.resolve("Already resolved");
promise.then(() => console.log('ES6 promise handled'));  // This will be lazy-loaded and run after current cycle
console.log("This runs first");  // Even though the promise is resolved, this will log first
```

This outputs:
```
This runs first
ES6 promise handled
```

## Benefits of Lazy Loading with Thenables

Lazy loading of callbacks in ES6 Promises offers several key advantages:

1. **Consistent Asynchronous Behavior**: The behavior of ES6 Promises is always consistent, regardless of when you attach your `then` or `catch` callbacks. Even if a promise is resolved before attaching a callback, the function will still be deferred until the next microtask queue is processed.

2. **Improved Performance**: Lazy loading ensures that unnecessary operations are avoided, as the callbacks only run when needed — that is, when the promise settles (resolves or rejects). This can lead to more efficient resource usage in large-scale asynchronous applications.

3. **Predictable Execution**: With lazy evaluation, developers can reason about their code execution more easily, ensuring that asynchronous actions happen only after the necessary events (like resolution or rejection of a promise) occur.

4. **Interoperability**: Since any object with a `then` method can be treated like a promise, libraries can still offer custom implementations or lightweight thenables while benefiting from the lazy loading of callbacks, as long as they follow the `thenable` pattern.

## Conclusion

ES6 thenables revolutionized how JavaScript handles asynchronous operations, providing developers with a **lazy-loaded** callback mechanism that ensures consistency, performance, and predictability. Unlike older implementations like jQuery’s Deferred objects, ES6 Promises ensure that callbacks are deferred until absolutely necessary, which can make asynchronous workflows both easier to manage and more efficient.

Understanding the difference between eager and lazy evaluation in async code is essential for writing clean, maintainable JavaScript, and ES6 thenables provide a robust solution for this challenge.

*Last* [Understanding JavaScript Promises and Lazy Loading Callbacks]('/posts/javascript-promises-and-thenables')

