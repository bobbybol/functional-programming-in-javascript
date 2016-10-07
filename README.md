# Functional Programming in JavaScript

A(n opinionated) summary of functional programming features in JavaScript

## First class functions

## Higher-order functions

### Filter

### Map

### Reduce

First we'll be exploring the higher-order functions native to JavaScript.

```javascript

if (true){
    let favoriteColor = "red";
    return "oh no it's bluuuuuuueeeeeeeeeeeeeeee...";
}

```

## Closures
Like objects, closures are a mechanism for containing state. In JavaScript, a closure is created whenever a function accesses a variable defined outside the immediate function scope. It’s easy to create closures: Simply define a function inside another function, and expose the inner function, either by returning it, or passing it into another function. The variables used by the inner function will be available to it, even after the outer function has finished running.

You can use closures to create data privacy in JavaScript using a factory function:
```javascript
var counter = function counter() {
    var count = 0;
    return {
        getCount: function getCount() {
            return count;
        },
        increment: function increment() {
            count += 1;
        }
    };
};
```

## Simple lamba syntax

