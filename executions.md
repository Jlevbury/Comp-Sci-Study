## Execution contexts

**1. Call-Back Queue**

In JavaScript, functions that take a long time to execute (like fetching data from a server) are often asynchronous. This means they're non-blocking: JavaScript doesn't wait for the function to finish before moving on to the next line of code. Instead, these functions are often provided with a callback function to execute once they've finished.

But when does this callback function get executed? This is where the callback queue (or task queue) comes in.

Here's a simplified view of how JavaScript's event loop, call stack, and callback queue interact:

1. When an asynchronous function is called, it's added to the call stack.
2. The asynchronous function starts running. Because it takes a while to complete, it's taken off the stack so other code can run.
3. When the asynchronous function is done, it puts its callback function into the callback queue.
4. If the call stack is empty, the event loop adds the first function in the callback queue to the call stack.
5. This function is then executed.

**2. Higher-Order Functions**

In JavaScript, functions are first-class citizens. They can be assigned to variables, stored in data structures, passed as arguments to other functions, and even returned as values from other functions.

A higher-order function is a function that takes one or more functions as arguments, returns a function as its result, or both. Higher-order functions are a key component of functional programming in JavaScript.

Example:
```javascript
// A simple higher-order function
function greet(name) {
  return function() {
    console.log(`Hello, ${name}`);
  };
}

let sayHelloJohn = greet('John');
sayHelloJohn(); // Outputs: "Hello, John"
```

**3. Closures**

In JavaScript, a closure is a function that has access to its own scope, the outer function's scope, and the global scope. This allows the inner function to access variables from an outer function even after the outer function has finished running.

Example:
```javascript
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log('outerVariable:', outerVariable);
    console.log('innerVariable:', innerVariable);
  }
}

let newFunction = outerFunction('outside');
newFunction('inside'); // Logs: "outerVariable: outside" and "innerVariable: inside"
```

**4. Factory Functions**

A factory function is a function that returns an object when it's called, and it's capable of producing object instances without the use of a class. This is another important concept in functional programming.

Example:
```javascript
function createPerson(name, age) {
  return {
    name,
    age,
    sayHello() {
      console.log(`Hello, my name is ${this.name}`);
    }
  };
}

let john = createPerson('John', 25);
john.sayHello(); // Outputs: "Hello, my name is John"
```

**5. Factory Functions vs. Constructor Functions**

A factory function returns an object and can be called directly. A constructor function is used with the `new` keyword and it doesn't explicitly return anything, but it implicitly returns `this` (the new object).

Example:
```javascript
// Factory function
function createPerson(name, age) {
  return {
    name,
    age
  };
}

// Constructor function
function Person(name, age) {
  this.name = name;
  this.age = age;
}

let john1 = createPerson('John', 25);
let john2 = new Person('John', 25);
console.log(john1, john2); // Both output: { name: 'John', age: 25 }
```

**6. Event Delegation Handling**

Event delegation is a technique in JavaScript where you delegate one event listener to a parent element instead of setting an event listener for each child element. The listener analyzes bubbled events to find a match on child elements.

This technique can be very beneficial for performance when dealing with a large number of similar elements, like list items, and when adding or removing elements dynamically.

Example:
```javascript
document.querySelector('#parent-element').addEventListener('click', function(event) {
  if(event.target.matches('#child-element')) {
    console.log('Child element clicked');
  }
});
```
Certainly, we can add those two topics to our list.

**7. Global Execution Context**

In JavaScript, whenever the JavaScript engine runs your code, it creates something known as an Execution Context. There are two types of Execution Context: Global Execution Context (GEC) and Functional Execution Context (FEC).

The Global Execution Context is created by the JavaScript engine as soon as you start a script. There's only one Global Execution Context in a particular run. This GEC is used to interpret code that isn't inside any functions. As there's only one global context, variables defined here will be accessible everywhere in the application.

For example:

```javascript
let globalVar = "I'm a global variable";

function sayHello() {
  console.log("Hello, world!");
}

console.log(globalVar); // This is executed in the global execution context
```

In the above example, `globalVar` and `sayHello()` are defined in the global execution context.

**8. Functional Execution Context**

Apart from the Global Execution Context, every time a function is invoked, the JavaScript engine creates a new Functional Execution Context for that function. 

Each function has its own execution context. This context is temporary and will be destroyed as soon as the function has finished executing.

The functional execution context is important because it forms a crucial part of closure — the function together with its lexical environment (the state when the function was declared).

For example:

```javascript
let globalVar = "I'm a global variable";

function sayHello() {
  let functionVar = "I'm a function variable";
  console.log(functionVar);
}

sayHello(); // This will create a new functional execution context
```

In the above example, when `sayHello()` is invoked, a new Functional Execution Context is created. The variable `functionVar` is defined in this context.

