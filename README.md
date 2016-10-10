# Functional Programming in JavaScript

A(n opinionated) summary of functional programming features in JavaScript

## What is functional programming?
There's a lot of complex explanations out there, and it's hard to capture all that functional programming _is_, but as the purpose of this document is to communicate ideas clearly and in simple terms, I'll start with a simple list of what functional programming has come to mean to me:
- juggling functions around:
  - passing functions as arguments to other functions
  - functions returning other functions
- keeping it DRY:
  - replacing repetitive logic with a simple function
  - largely eliminating the need for `for` loops
- letting go of code micromanagement:
  - working on streams of data rather than discrete data
  - a
- writing code that's easy for others to read and reason about

## Why do we want functional programming?
Simply put, mastering functional programming will let you write your code with less bugs, in less time.
Less bugs because your code is easier to reason about.
Less time because you will be able to re-use more of your code.

Functional programming glossaries contain a large number of large words, but at its core, the essence of FP is really very simple; programs are built mostly with a handful of very small, very reusable, very predictable pure functions.

Pure functions have a few properties that make them extremely reusable and extremely useful for a variety of applications:

### Idempotence: 
Given the same inputs, a pure function will always return the same output, regardless of the number of times the function is called. This also serves the very useful purpose of separating computation from dependency on both time and order of operations.

### Free from side-effects
Pure functions can be safely applied with no side-effects, meaning that they do not mutate any shared state or mutable arguments, and other than their return value, they don’t produce any observable output.

### Reactive programming 
Uses functional utilities like map, filter, and reduce to create and process data flows which propogate changes through the system: hence, reactive. When input x changes, output y updates _automatically_ in response.

## Lists
Lists of data to manipulate

## Streams
Streams are simply lists expressed over time.

## First class functions
Functions are values.
```javascript
var quadruple = function (x) {
  return x * 4;
};
```

## Higher-order functions
Because functions are values in JavaScript, they can be passed to other functions. These functions we call 'higher-order functions'. Higher-order functions are useful because you can essentially create a number of small, simple, easy-to-reason-about functions the can be **composed** into bigger functions to create more complex functionality.

JavaScript has some very useful higher-order functions built-in:

### Filter
Filter is very simple and extremely useful. 
Filter is a function on the array.
Filter accepts another function as its argument.
Filter will use the other function to return a new, filtered version of the array.

```javascript
let felines = [
  { name: 'mufasa', subspecies: 'alion' },
  { name: 'shere khan', subspecies: 'atiger' },
  { name: 'hobbes', subspecies: 'atiger' },
  { name: 'dassler', subspecies: 'apuma' },
  { name: 'adestra', subspecies: 'alynx' },
  { name: 'lumachina', subspecies: 'acheetah' },
  { name: 'ugo', subspecies: 'akittycat' }
]

// find tigers
// with a for loop
let tigers = [];
for (let i = 0; i < felines.length; i++) {
  if (felines[i].subspecies === 'atiger') {
    tigers.push(felines[i]);
  }
}

// find tigers
// with the filter function
let tigers = felines.filter(function(feline) {
  return feline.subspecies === 'atiger';
}
```

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

