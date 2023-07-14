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

## Callback Queue in-depth
 **Callback Queue** and its role in the JavaScript event loop.

JavaScript is single-threaded, which means it executes one operation at a time, from a single call stack. So, what happens when we have a function that takes a while to complete, such as a network request or a `setTimeout`? We don't want to block the thread and halt the execution of the rest of our code.

This is where the JavaScript event loop, call stack, and callback queue come into play. These mechanisms allow JavaScript to handle asynchronous operations and callbacks in a non-blocking way.

**Event Loop**

The event loop is a constantly running process that checks if the call stack is empty. If it's empty, it will take the first item from the callback queue and push it onto the call stack, which effectively runs it.

**Callback Queue (also known as the Task Queue)**

The callback queue is a list of all the callbacks that are ready to be executed. When an asynchronous operation finishes and its callback is ready to be executed, it's added to the callback queue.

**Call Stack**

The call stack is where the JavaScript engine keeps track of where it is in the code. If a function is called, it's added to the top of the stack. If a function returns, it's removed from the top of the stack. If the stack is empty, the event loop can add a function from the callback queue.

Here's a step-by-step example of how these interact:

1. When the JavaScript engine runs your code, it first enters the Global Execution Context and goes through your code line by line.

2. When it encounters an asynchronous function, it sends this operation to the corresponding API (like the Timer API for `setTimeout`, or the Fetch API for network requests).

3. While the async operation is running, the JavaScript engine continues going through the rest of your code. The async function is essentially "set aside" to finish.

4. When the async operation is finished, it's callback function is added to the callback queue.

5. The event loop is constantly checking if the call stack is empty. Once the call stack is empty, the event loop adds the first function from the callback queue to the call stack.

6. The callback function is then executed.

Here's a simple example:

```javascript
console.log("First");

setTimeout(() => {
  console.log("Second");
}, 0);

console.log("Third");
```

In this example, you might expect "First", "Second", "Third" to be logged because of the `setTimeout` delay of `0`. However, the actual result will be "First", "Third", "Second". This is because `setTimeout` is an asynchronous function. Even though its delay is `0`, it's callback is still added to the callback queue and only run when the call stack is empty.

This is a basic overview of the callback queue. It's a fundamental part of understanding how JavaScript handles asynchronous operations and callbacks. 
Great, let's explore **Higher-Order Functions** in more depth.

## High Order functions In-depth

In JavaScript, functions are first-class citizens, meaning they can be assigned to variables, stored in data structures, passed as arguments to other functions, and even returned as values from other functions. This is a fundamental concept in JavaScript and forms the basis of functional programming in the language.

A higher-order function is a function that takes one or more functions as arguments, returns a function as its result, or both. 

Here are some more in-depth examples and use cases of higher-order functions:

**1. Functions that accept other functions as arguments**

Many array methods are higher-order functions because they take a function as an argument.

Example with Array's `map` method:
```javascript
let numbers = [1, 2, 3, 4, 5];

// 'map' is a higher order function that takes a function as an argument
let squares = numbers.map(function(number) {
  return number * number;
});

console.log(squares); // [1, 4, 9, 16, 25]
```

Example with Array's `filter` method:
```javascript
let numbers = [1, 2, 3, 4, 5];

// 'filter' is a higher order function that takes a function as an argument
let evenNumbers = numbers.filter(function(number) {
  return number % 2 === 0;
});

console.log(evenNumbers); // [2, 4]
```

**2. Functions that return other functions**

You can also have higher-order functions that return other functions.

Example:
```javascript
function greaterThan(n) {
  return function(m) {
    return m > n;
  };
}

let greaterThan10 = greaterThan(10);
console.log(greaterThan10(11)); // true
```

In the above example, `greaterThan` is a higher-order function because it returns a function.

**3. Functions that do both**

And of course, you can have higher-order functions that both take functions as arguments and return a function.

Example:
```javascript
function not(fn) {
  return function(argument) {
    return !fn(argument);
  };
}

let isOdd = function(n) {
  return n % 2 === 1;
};

let isEven = not(isOdd);
console.log(isEven(4)); // true
```

In the above example, `not` is a higher-order function because it both takes a function as an argument (`isOdd`) and returns a function.

Higher-order functions are a key part of JavaScript and provide the foundation for techniques such as functional programming and callback functions. Understanding them will give you a greater understanding of how JavaScript works.

## Closures In-depth
 **Closures**. 

A closure in JavaScript is a function that has access to its own scope, the outer function's scope, and the global scope. More specifically, a closure gives you access to an outer function’s scope from an inner function.

Let's see this in action with an example:

```javascript
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log('outerVariable:', outerVariable);
    console.log('innerVariable:', innerVariable);
  }
}

const newFunction = outerFunction('outside');
newFunction('inside'); // Logs: outerVariable: outside, innerVariable: inside
```

In this example, `innerFunction` has access to its own scope (the `innerVariable`), the outer function's scope (the `outerVariable`), and the global scope.

When we invoke `outerFunction('outside')`, it returns the `innerFunction` with access to `outerVariable` from the `outerFunction`'s scope, even after `outerFunction` has finished executing. When we later call `newFunction('inside')`, it still has access to the `outerVariable`. This is the fundamental concept of a closure.

Closures are a powerful feature in JavaScript because they allow you to control what is and isn't in the scope of a function, and they also allow you to associate data (environment) with a function that operates on that data, which is a key aspect of functional programming.

Closures are widely used in JavaScript for object data privacy, in event handlers and callback functions, and in function factories, module patterns, and many other advanced JavaScript patterns.

## Factory vs Constructor Functions
 **Factory Functions and Constructor Functions**.

Both factory and constructor functions are used to create objects in JavaScript. However, they do so in different ways.

**Constructor Functions**

Constructor functions use the `new` keyword to create new objects. The name of a constructor function usually starts with a capital letter to distinguish it from a regular function.

Here is an example of a constructor function:

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.introduce = function() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  };
}

const person1 = new Person('Alice', 25);
const person2 = new Person('Bob', 30);

person1.introduce(); // "Hello, my name is Alice and I am 25 years old."
person2.introduce(); // "Hello, my name is Bob and I am 30 years old."
```

In the example above, `Person` is a constructor function. When we call it with the `new` keyword, it creates a new object, sets the `this` keyword to the new object, and then returns `this`.

**Factory Functions**

As we just discussed, factory functions create and return objects. They do not require the use of the `new` keyword.

```javascript
function createPerson(name, age) {
  return {
    name: name,
    age: age,
    introduce() {
      console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
    }
  };
}

const person1 = createPerson('Alice', 25);
const person2 = createPerson('Bob', 30);

person1.introduce(); // "Hello, my name is Alice and I am 25 years old."
person2.introduce(); // "Hello, my name is Bob and I am 30 years old."
```

**Key Differences**

1. Constructors (when called with `new`) create a unique object of a particular type, with its own separate properties. Factory functions return a new object literal, often even using a new object of the same literal for each product.

2. Constructors make use of the `this` keyword and do not explicitly return anything. Factory functions return an object.

3. Constructors, when used with the `new` keyword, create an object that inherits from the object defined in the constructor's `prototype` property. Objects created with factory functions can implement inheritance in other ways, or not at all, and can have more flexibility in object creation.

4. Constructors enforce the use of the `new` keyword (if you forget it, `this` will not refer to the new object instance in non-strict mode). Factory functions are just regular functions that return an object and do not require the use of `new`.

In many cases, the choice between factory and constructor patterns comes down to personal preference and the specific needs of your project. It's important to understand both patterns as a JavaScript developer, since different code bases and libraries might use one or the other.

## Event Delegation

**Event Delegation**.

Event delegation is a technique in JavaScript that takes advantage of event bubbling to handle events at a higher level in the DOM than the element on which the event happened. It allows us to attach a single event listener, to a parent element, that will fire for all descendants matching a selector, whether those descendants exist now or are added in the future.

To better understand this, let's take a look at an example:

HTML:
```html
<ul id="todo-list">
  <li class="item">Walk the dog</li>
  <li class="item">Go to the gym</li>
  <li class="item">Buy groceries</li>
</ul>
```

JavaScript:
```javascript
let todoList = document.getElementById('todo-list');

todoList.addEventListener('click', function(event) {
  let targetElement = event.target;

  // We check if the clicked element is an item in the list
  if (targetElement.classList.contains('item')) {
    console.log(`You clicked on item: ${targetElement.textContent}`);
  }
});
```

In this example, we're using event delegation to add a single 'click' event listener to the `ul` element. When an `li` element within the `ul` is clicked, the event bubbles up to the `ul`, where our event listener is triggered. We can then inspect the `event.target` to see which element was actually clicked.

One of the main benefits of event delegation is performance. Instead of adding event listeners to each individual `li` (which could be a huge number in a large application), we only have one event listener on the `ul`. This can significantly reduce memory usage and improve performance.

Event delegation also works for elements that are added to the page dynamically, after the event listener is set up. For example, if we were to add another `li` to our `ul`, the event listener would work for that `li` just as it does for the existing ones, without us having to add another event listener.

## Global Execution Context In-depth
 **Global Execution Context**.

In JavaScript, every line of code that runs does so in an environment called an execution context. The Global Execution Context (GEC) is the default or base execution context. The global execution context is the outermost one where variables that are not inside any function (and hence are globally accessible) are declared.

When a JavaScript engine (like V8 in Chrome) runs a script, it creates a global execution context. Two things happen at this stage:

1. **Creation Phase:** In this phase, the function declarations are saved in memory, and the variable declarations are set to `undefined`. This process is often called "hoisting". It's also worth noting that in the creation phase, a global object (like `window` in a browser environment), `this`, and outer environment (reference to the outer scope, but for GEC it's `null` because it's the outermost context) are also created.

2. **Execution Phase:** In this phase, the code is executed line by line and the variable declarations, if there are any, are replaced with the actual values.

Let's take a simple example:

```javascript
console.log(myVar); // undefined, not ReferenceError because of hoisting
myVar = 5; // assign 5 to myVar
console.log(myVar); // 5
```

Here, `myVar` is declared in the global execution context. In the creation phase, it's set to `undefined`. In the execution phase, it's reassigned to `5`.

That's a high-level overview of the global execution context in JavaScript. There's a lot more to this topic, especially when we start talking about function execution contexts and how they interact with the global execution context.

**Common coding scenarios**

As mentioned earlier, every line of code in JavaScript runs in an environment called an execution context. When JavaScript starts to execute a script, it first creates a global execution context.

Now, let's consider a scenario where we have some functions in our code. 

```javascript
var globalVar = "I'm a global variable";

function firstFunc() {
  var firstVar = "I'm in firstFunc";
  
  function secondFunc() {
    var secondVar = "I'm in secondFunc";
    console.log(globalVar, firstVar, secondVar);
  }
  
  secondFunc();
}

firstFunc();
```

When we call `firstFunc`, a new execution context, the `firstFunc` execution context, is created and pushed onto the execution stack. This new context has a reference to its outer environment, which is the global execution context. That's why `firstFunc` can access `globalVar`. 

Inside `firstFunc`, we call `secondFunc`, which creates another new execution context, the `secondFunc` execution context. This is again pushed onto the execution stack. The `secondFunc` execution context's outer environment is `firstFunc`, so `secondFunc` can access `firstVar` as well as `globalVar`.

This structure of execution contexts is what makes JavaScript have function-level scope. Each function creates a new scope, and each function can access variables declared in its own scope as well as any variable in any of its outer scopes.

When `secondFunc` finishes executing, its execution context is popped off the execution stack, and we go back to the `firstFunc` context. When `firstFunc` finishes, its execution context is also popped, and we go back to the global execution context. 

You encounter execution contexts anytime you're working with JavaScript, even if you're not explicitly aware of them. Understanding them helps you understand how JavaScript handles scoping, hoisting, the `this` keyword, closures, and more.

## Functional Execution Context
 **Functional Execution Context**
 
Every line of code in JavaScript runs in an environment called an execution context. The functional execution context is the environment in which function code is executed.

Let's go over the creation of a functional execution context step by-step:

1. **Activation Object/Variable Object Creation:** The first stage of a functional execution context is the creation of an activation object, also known as a variable object. The activation object is filled with arguments passed to the function, declared variables, and function declarations.

2. **Creation of Scope Chain:** In the next phase, JavaScript creates a scope chain. The scope chain is used for variable resolution. If a variable is not found in the current scope, JavaScript looks up the chain to find it in the outer environment's scope. This process continues until the variable is found or the global scope is reached. If the variable is not found in the global scope, a `ReferenceError` is thrown.

3. **Determine the value of `this`:** The final step in the creation phase is determining the value of `this`. In a regular function, `this` refers to the global object. However, if the function is a method (i.e., a function that is a property of an object), `this` refers to the object the method was called on. In strict mode, `this` is `undefined` for regular functions.

After the creation phase, the function enters the **execution phase**, where the code is executed line by line.

Let's take an example:

```javascript
function greet(name) {
  var greeting = 'Hello';
  console.log(greeting + ' ' + name);
}

greet('Alice');
```

When the `greet` function is called, a new functional execution context is created. In the creation phase, the activation object is filled with the `name` argument and the `greeting` variable. The scope chain is created, linking the `greet` function's scope to the global scope. And `this` is determined to be the global object (or `undefined` in strict mode).

In the execution phase, the code inside the `greet` function is executed line by line.

Understanding the functional execution context can help you understand how JavaScript executes function code and handles scoping, hoisting, and the `this` keyword.

**Common use occurences**

Consider an application where users can view and edit a list of tasks. Let's say we have a function `updateTask` that is used to update a task in the database and then update the task displayed on the webpage. Here's how it might look:

```javascript
function updateTask(taskId, updatedText) {
  // This would actually make an API call to your server to update the task
  // in the database. For this example, we'll just log a message.
  console.log(`Updating task with ID ${taskId} in the database`);

  // Now we need to update the task in the webpage.
  var taskElement = document.getElementById(taskId);
  taskElement.textContent = updatedText;
}
```

When `updateTask` is called, a new functional execution context is created. The activation object includes the `taskId` and `updatedText` arguments, and the `taskElement` variable. The scope chain links the `updateTask` context to the global context. The value of `this` is determined, which in this case would be the global object (`window` in a browser) because `updateTask` is not a method on an object.

The code in the function is then executed line by line. The `console.log` statement runs, then the `document.getElementById` line runs, and finally the `taskElement.textContent` line runs.

By understanding functional execution contexts, you can better understand what is happening behind the scenes when this function is called. You can understand how JavaScript is handling the variables and arguments, how it determines the value of `this`, and why, for example, the `taskId` and `updatedText` variables are not available globally (because they are in the `updateTask` execution context, not the global context).

Knowing how functional execution contexts work is particularly important when you start dealing with asynchronous JavaScript, because callbacks and promises can create new execution contexts that affect the flow of your code.

