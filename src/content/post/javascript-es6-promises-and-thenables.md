---
publishDate: "24 Oct 2024"
title: "Understanding JavaScript Promises"
description: "To understand Promises, it is important to understand what exactly thenables are."
excerpt: "To put it simply: a thenable is any object that implements a then method, regardless of whether it is a Promise."
tags: ["JavaScript", "ECMAScript 2015 (ES6)", "lazy-loading", "asynchronous"]
coverImage:
    src: "../../assets/jses6_logo.png"
    alt: "JavaScript ES6 Logo"
---

In JavaScript, the concept of **thenables** often arises when working with Promises. Promises inherit from the base class Thenable, meaning that Promises are a type of Thenable, but a Thenable is not necessarily a promise. To understand Promises, it’s important to understand what exactly thenables are and how they fit into the world of asynchronous programming.

## What is a Thenable?

A *thenable* is an object or function that has a `then` method. This method works similarly to the `then` method in a JavaScript Promise. The term comes from the fact that such objects or functions can be "then-ed" — meaning they have a `then` method that allows you to handle resolved or rejected values.

To put it simply: **a thenable is any object that implements a `then` method, regardless of whether it is a Promise**. Thenables can be used in many of the same ways as promises because they provide the same basic interface.

## Example of a Thenable

Here's an example of a basic thenable object:

```javascript
const thenable = {
  then: function(resolve, reject) {
    // Simulate asynchronous behavior
    setTimeout(() => resolve("Thenable resolved"), 1000);
  }
};
```

This object can be passed to anything expecting a Promise-like object, such as JavaScript's native `Promise.resolve()`. The `then` method accepts two arguments: a `resolve` function and a `reject` function, which are used to indicate whether the asynchronous task was successful or not.

```javascript
Promise.resolve(thenable).then(result => {
  console.log(result); // Outputs "Thenable resolved" after 1 second
});
```

In this example, the `then` method of our thenable object behaves just like a Promise's `then` method. After 1 second, it resolves with the string "Thenable resolved", which is then logged to the console.

## Promises vs Thenables

While all promises are thenables, not all thenables are promises. A promise is a specific implementation of the thenable pattern, with well-defined behavior for state transitions (pending, resolved, or rejected) and chaining. A thenable, on the other hand, can be any object that follows the `then` method pattern, but it might not strictly adhere to the full specification that promises follow.

Promises automatically handle state transitions and guarantee certain behaviors like:

- **Immutability of state**: Once a promise is resolved or rejected, it stays in that state.
- **Error handling**: Promises have well-defined mechanisms for handling rejection and errors.

Thenables, being less structured, might not follow these rules strictly. For instance, the `then` method of a thenable might be manually implemented in a way that doesn't behave like a promise under certain conditions.

## Why Use Thenables?

Thenables are useful because they allow objects to integrate into Promise-based workflows without being full-blown promises. Libraries or frameworks might expose thenables to allow interoperability with promises while maintaining flexibility. A common reason to use a thenable instead of a promise is to avoid the overhead of creating a full Promise object, especially if the object already has asynchronous logic and only needs to expose a `then` method.

For example, some libraries like jQuery used to provide thenable-like structures (e.g., `$.ajax()` returned a Deferred object with a `then` method) before native promises became widely used.

## Implementing a Custom Thenable

Let’s take a look at how you might implement your own thenable:

```javascript
class CustomThenable {
  constructor(value) {
    this.value = value;
  }

  then(resolve, reject) {
    setTimeout(() => {
      if (this.value) {
        resolve(this.value);
      } else {
        reject("No value provided");
      }
    }, 1000);
  }
}

const myThenable = new CustomThenable("Hello, Thenable!");

Promise.resolve(myThenable).then(result => {
  console.log(result); // Outputs "Hello, Thenable!" after 1 second
}).catch(error => {
  console.error(error);
});
```

In this example, we create a class `CustomThenable` that implements the `then` method. Depending on whether the `value` property is set, it will resolve or reject after 1 second.

## Using Thenables with Native JavaScript Promises

JavaScript promises are designed to interoperate with any thenable. If you pass a thenable object to `Promise.resolve()`, it will behave as if you passed a real promise:

```javascript
const thenable = {
  then: function(resolve, reject) {
    resolve("Thenable worked!");
  }
};

Promise.resolve(thenable).then(result => {
  console.log(result); // Outputs "Thenable worked!"
});
```

In this case, `Promise.resolve()` checks if the object has a `then` method. If it does, the promise will wait for the thenable to resolve or reject. This makes thenables an excellent mechanism for working with both promise-based APIs and older, non-promise-based libraries.

## Conclusion

Thenables are an important concept in JavaScript because they allow any object with a `then` method to participate in promise chains. While promises are more robust and offer guarantees about state transitions and error handling, thenables offer flexibility and can be useful for integrating older code or custom asynchronous behavior with modern promise-based workflows.

Understanding thenables helps demystify the behavior of JavaScript promises and allows developers to create objects that can work seamlessly with promise chains without necessarily adhering to the full promise specification.


*NEXT* [Understanding JavaScript Promises and Lazy Loading Callbacks]('/posts/javascript-promises-and-lazy-loading-callbacks')

