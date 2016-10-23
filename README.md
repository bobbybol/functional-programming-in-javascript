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
Filter is a very simple and useful function; it can be called on an array and will return a filtered version of that array. Filter accepts another function as its argument: when this callback function returns `true` while iterating over an element of the array, that element is pushed into a new array. If the function returns false, the current array element is ignored.

```javascript
let felines = [
  { name: 'mufasa', subspecies: 'alion' },
  { name: 'shere khan', subspecies: 'atiger' },
  { name: 'hobbes', subspecies: 'atiger' },
  { name: 'dassler', subspecies: 'apuma' },
  { name: 'adestra', subspecies: 'alynx' },
  { name: 'lumachina', subspecies: 'acheetah' },
  { name: 'ugo', subspecies: 'akittycat' }
];

// find tigers
// we could do it with a for loop
let tigers = [];
for (let i = 0; i < felines.length; i++) {
  if (felines[i].subspecies === 'atiger') {
    tigers.push(felines[i]);
  }
}

// find tigers
// but with the filter function it takes less code
let tigers = felines.filter(function(feline) {
  return feline.subspecies === 'atiger';
};

// find tigers
// and we can even break up the code to make it more reusable
let isTiger = function(feline) {
  // the isTiger function returns true if we pass it atiger
  return feline.subspecies === 'atiger'
};

let tigers = felines.filter(isTiger);
```

### Map
Map is another higher-order function that works on the array. Unlike filter, map doesn't throw any of the original array's elements away, instead it transforms them. Map creates a new array with the results of calling a function for every array element. The map method calls the provided function once for each element in an array, in order.

```javascript
let felines = [
  { name: 'mufasa', subspecies: 'alion' },
  { name: 'shere khan', subspecies: 'atiger' },
  { name: 'hobbes', subspecies: 'atiger' },
  { name: 'dassler', subspecies: 'apuma' },
  { name: 'adestra', subspecies: 'alynx' },
  { name: 'lumachina', subspecies: 'acheetah' },
  { name: 'ugo', subspecies: 'akittycat' }
];

// find all felines' names
// we could do it with a for loop
let namess = [];
for (let i = 0; i < felines.length; i++) {
  names.push(animals[i].name);
}

// find all felines' names
// with the map method (much shorter!)
let names = felines.map(function(feline) {
  return feline.name;
});

// find all felines' names
// with es6 arrow functions (even shorter!)
let names = felines.map((x) => x.name);
```

### Reduce
Where filter and map (and find and reject) are very specific about the way they transform a list of items, _reduce_ can be considered to be the 'multitool' of list transformations. In it's most common application, the reduce method reduces the array to a single value. The reduce method executes a provided function for each value of the array (from left-to-right). The return value of the function is stord in an accumulator (result/total).

**Note that we have to pass a second argument to the reduce method (besides the callback function), which is the initial value.**

**Also note that now the callback function takes additional arguments as well, where the first argument is actually the total of the items being 'reduced', and the _second_ argument is the item in the array currently being iterated over.**

```javascript
let observedAlions = [
  { day: 'mon', amount: 19 },
  { day: 'tue', amount: 20 },
  { day: 'wed', amount: 31 },
  { day: 'thu', amount: 40 },
  { day: 'fri', amount: 11 }
];

// add all observations to a single total amount
// we could do it with a for loop
let totalObservations = 0;
for (let i = 0; i < observedAlions.length; i++) {
  totalObservations += orders[i].amount;
}

// the following demonstrates how reduce reduces an array to a single number:
let totalObservations = observedAlions.reduce(function(sum, dailyRecord){
  return sum + dailyRecord.amount;
}, 0);
```

Reduce is not limited to reducing a list to a number, it can reduce it to anything, such as another array, or an object. 

## Closures
Like objects, closures are a mechanism for containing state. In JavaScript, a closure is created whenever a function accesses a variable defined outside the immediate function scope. It’s easy to create closures: Simply define a function inside another function, and expose the inner function, either by returning it, or passing it into another function. The variables used by the inner function will be available to it, even after the outer function has finished running.

The simplest example of a closure uses a global variable outside its own scope:
```javascript
let outer = 10;

function innerPlusOuter() {
  let inner = 11;
  return outer + inner;
}
```
Where innerPlusOuter is using outer to close its own scope.

> Closures are nothing but **functions with _preserved data_**

You can use closures to create data privacy in JavaScript using a factory function:
```javascript
let counter = function counter() {
  let count = 0;
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

## Partial application vs. Currying

## Recursion
A pretty interesting example of functions calling other functions is recursion - where a function calls _itself_.
The function keeps calling itself, until it doesn't; meaning that there must be an 'exit strategy' to stop the function from calling itself indefinitely.

```javascript
// Let's create a function that counts down from the number passed as its argument.
// So `countDownFrom(10)` would output
// 10
// 9
// 8
// ...
// 1

let countDownFrom = (number) => {
  // Exit strategy first..
  if (number === 0) {
    return;
  }
  
  // ..then just output number..
  console.log(number);
  
  // ..and call on `countDownFrom` again with a changed argument
  countDownFrom(number - 1);
};
```

### Why is recursion useful?
Every time you use a `for` loop, you could potentially use recursion instead.
But it doesn't work the other way around because there are things that recursion can do that loops cannot.

## Promises
We all know callbacks, which say: "when **this** thing is done, execute **that** piece of code."
Promises serve that same purpose, but promises are a bit more powerful, because they are _composable_.

A very basic promise:
```javascript
import loadImagePromised
from './load-image-promised';

// `whenImageLoaded` is a promise
let whenImageLoaded = loadImagePromised('images/a-cute-lion.png');

// When the promise is fulfilled, THEN execute the callback function
whenImageLoaded.then( (img) => {
  // The callback function creates an element..
  let imgElement = document.createElement("IMG");
  
  // ..and sets the source of the element to the image loaded..
  imgElement.src = img.src;
  
  // ..and appends the element to the body.
  document.body.appendChild(imgElement);
});
```

ECMAScript 6 supports promises natively:
```javascript
function loadImage(url) {
  return new Promise((resolve, reject) => {
    let image = new Image();
    
    image.onload = function() {
      resolve(image);
    };
    
    image.onerror = function() {
      let message = 'Could not load image at ' + url;
      reject(new Error(message);
    };
    
    image.src = url;
    
  });
}
```

## Simple lamba syntax

