# Comp-Sci-Study
Reference material for Algorithm efficiency and measurement
## Overview
## Useful Links 

https://www.bigocheatsheet.com/

https://www.cs.usfca.edu/~galles/visualization/Search.html

**1. Big O notation**



Big O notation is a way to convey how well a computer algorithm scales as the number of data it operates on increases. It provides an upper bound of the complexity in the worst-case scenario, helping to quantify performance as the input size becomes extremely large.

Let's take a few examples:

- **O(1)**: This is called "constant time." No matter how big our input is, the time (or the number of operations) it takes to perform the operation is constant. For instance, accessing an element in an array by its index.

- **O(n)**: This is called "linear time." Here, the time it takes to perform an operation will grow linearly with the input data. For example, if you have to print out every element in an array, you have to visit each element once.

- **O(n²)**: This is called "quadratic time." The time it takes to do something is proportional to the square of the number of items. An example of an O(n²) operation is the bubble sort algorithm for sorting an array.

- **O(log n)**: This is called "logarithmic time." The time it takes to do something decreases with each operation. An example would be binary search on a sorted array.

**2. Data Structures**

Data structures are a way of organizing and storing data so they can be accessed and worked with efficiently. They define the relationship between the data, and the operations that can be performed on the data. Here are a few common ones:

- **Arrays:** An array is a collection of elements identified by index or key. The elements are stored in contiguous memory locations.

- **Linked Lists:** A linked list is a linear collection of data elements, whose order is not given by their physical placement in memory. Instead, each element points to the next.

- **Stacks & Queues:** A stack is a linear data structure which follows a particular order in which the operations are performed: LIFO (Last In First Out). A queue is similar, but the operation order is FIFO (First In First Out).

- **Trees:** A tree is a nonlinear data structure that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node.

- **Hash Tables:** A hash table, also known as a hash map, is a data structure that implements an associative array abstract data type, a structure that can map keys to values.

**3. Using Recursion in Functions**

Recursion is a method of solving problems that involves breaking a problem down into smaller and smaller subproblems until you get to a small enough problem that it can be solved trivially. It usually involves a function calling itself.

Here's an example using the factorial function, which is a classic example of a function where recursion can be used:

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n-1)
```

In this case, the `factorial` function calls itself to perform the calculation, and this continues until it reaches the base case (when `n` is `0`).

Remember, every recursive function should have the following characteristics:
- A simple base case (or cases) — a terminating scenario that does not use recursion to produce an answer.
- A set of rules, also known as recurrence relation that reduce all other cases towards the base case.

I hope this provides a good overview of these concepts. Feel free to ask any questions if something isn't clear!

## Big O 

**Big O Notation In-Depth**

The idea of Big O notation is to express how an algorithm scales based on input size. This is a way of approximating the complexity of an algorithm without getting into the nitty-gritty details of machine-level or low-level operations. Instead, we focus on how the algorithm's complexity grows with input size. This is also known as the algorithm's "order of growth."

Consider this example of a function that finds if a number exists in an array:

```javascript
function doesExist(array, num) {
    for(let i = 0; i < array.length; i++) {
        if (array[i] === num) {
            return true;
        }
    }
    return false;
}
```

The Big O notation of this function is O(n) where 'n' is the size of the array. The time complexity is linear because in the worst-case scenario, the function might have to look at every element in the array once (i.e., the number we are looking for is the last one in the array or does not exist in the array).

This is an important aspect of Big O notation: it expresses worst-case scenarios. In this example, even if the number is the first element of the array, the Big O notation is still O(n), because we are considering the worst-case scenario where the function would have to go through all elements of the array.

Here are some common time complexities you might encounter, ordered from most efficient to least efficient:

- **O(1):** Constant time. The algorithm takes the same amount of time to complete, regardless of the size of the input. An example of this would be accessing an element in an array by its index.

- **O(log n):** Logarithmic time. The algorithm splits the input data in each step, significantly reducing the size of the problem each time. Binary search is an example of a log n algorithm.

- **O(n):** Linear time. The running time increases at most linearly with the size of the input data. An example of this would be our `doesExist` function above.

- **O(n log n):** Linear-Logarithmic time. Many efficient sorting algorithms fall under this category, such as quicksort, heapsort, and mergesort.

- **O(n^2):** Quadratic time. The time taken by the algorithm is proportional to the square of the size of the input data. An example of this would be the bubble sort algorithm.

- **O(n^3):** Cubic time. The time taken is proportional to the cube of the size of the input data. This is common with simple algorithms for matrix multiplication.

- **O(2^n):** Exponential time. The values grow exponentially for an increase in input data size. This can be seen in many recursive algorithms like the naive Fibonacci sequence calculation.

- **O(n!):** Factorial time. These are the most time-consuming algorithms, and the time taken grows factorially with the size of the input data. An example of this would be the brute force search algorithm for the traveling salesman problem.





**Big O Notation in JavaScript**

1. **O(1): Constant Time Complexity**
Constant time complexity means that the running time of the function is constant; it does not depend on the size of the input.

Example:

```javascript
function getItem(array, index) {
  return array[index];
}
```

No matter how large the array is, it takes the same amount of time to return the item at a given index.

2. **O(n): Linear Time Complexity**
Linear time complexity means that the running time of the function grows linearly with the size of the input.

Example:

```javascript
function findMax(array) {
  let max = array[0];
  for(let i = 0; i < array.length; i++) {
    if(array[i] > max) {
      max = array[i];
    }
  }
  return max;
}
```

In the worst-case scenario, the function has to check each element of the array to find the maximum. So, the time complexity increases linearly with the size of the array.

3. **O(n²): Quadratic Time Complexity**
Quadratic time complexity means that the running time of the function is proportional to the square of the size of the input.

Example:

```javascript
function bubbleSort(array) {
  for(let i = 0; i < array.length; i++) {
    for(let j = 0; j < array.length - i - 1; j++) {
      if(array[j] > array[j + 1]) {
        // Swap array[j] and array[j + 1]
        let temp = array[j];
        array[j] = array[j + 1];
        array[j + 1] = temp;
      }
    }
  }
  return array;
}
```

Bubble sort involves comparing each element of the array with every other element. Thus, it has a time complexity of O(n²).

4. **O(log n): Logarithmic Time Complexity**
Logarithmic time complexity means that the running time of the function grows logarithmically with the size of the input.

Example:

```javascript
function binarySearch(array, x) {
  let start = 0, end = array.length - 1;

  while (start <= end) {
    let mid = Math.floor((start + end) / 2);

    if (array[mid] === x) // item found
      return mid;
    else if (array[mid] < x)
      start = mid + 1;
    else
      end = mid - 1;
  }

  return -1;
}
```

Binary search is a search algorithm that finds the position of a target value within a sorted array. It compares the target value to the middle element of the array; if they are unequal, the half in which the target cannot lie is eliminated, and the search continues for the remaining half until it succeeds. If the search ends with the remaining half being empty, the target is not in the array.

## Data Structures
**Data Structures**. 

Data structures allow you to organize data in a way that enables you to store collections of data, relate them, and perform operations on them accordingly.

Here are some of the most used data structures in JavaScript:

**1. Arrays**

An array in JavaScript is a high-level, list-like object which is used to store multiple values in a single variable.

```javascript
let arr = [1, 2, 3, 4, 5];
```
In an array, you can access elements by their indices, insert elements, remove elements and sort the array, among other operations.

```javascript
console.log(arr[0]); // Access the first element, prints: 1
arr.push(6); // Insert an element at the end
console.log(arr.pop()); // Remove the last element, prints: 6
console.log(arr.sort()); // Sort the array
```

**2. Objects (Associative Arrays)**

In JavaScript, an object is a standalone entity, with properties and type. It's similar to an associative array (a.k.a map, dictionary) in other languages.

```javascript
let obj = {
    "name": "John Doe",
    "age": 30,
    "email": "john@example.com"
};
```
You can access, add, update and delete properties from an object:

```javascript
console.log(obj.name); // Access property, prints: "John Doe"
obj.phone = "1234567890"; // Add property
obj.age = 31; // Update property
delete obj.email; // Delete property
```

**3. Sets**

A Set is a collection of values, where each value may occur only once.

```javascript
let set = new Set([1, 2, 3, 4, 5]);
```
You can add, delete and check if an item exists in the set, among other operations.

```javascript
set.add(6); // Add an element
set.delete(1); // Delete an element
console.log(set.has(2)); // Check if an element exists, prints: true
```

**4. Maps**

The Map object holds key-value pairs and remembers the original insertion order of the keys. A Map object iterates its elements in insertion order — a for...of loop returns an array of [key, value] for each iteration.

```javascript
let map = new Map();
map.set('name', 'John Doe'); // Add a value
console.log(map.get('name')); // Get a value, prints: "John Doe"
map.delete('name'); // Delete a value
```

**5. Stacks and Queues**

JavaScript does not have dedicated classes for Stack and Queue data structures, you can easily implement them using Arrays.

Stack (LIFO - Last In First Out):
```javascript
let stack = [];
stack.push(1); // Push item into the stack
console.log(stack.pop()); // Pop item from the stack
```

Queue (FIFO - First In First Out):
```javascript
let queue = [];
queue.push(1); // Enqueue item
console.log(queue.shift()); // Dequeue item
```

Each of these structures has its use cases, pros, and cons. The choice of data structure usually comes down to the specific problem you're trying to solve.

## Stacks and Queues. 
Even though JavaScript does not have dedicated classes for these data structures, you can implement them using arrays.

**Stack**

A stack is a linear data structure that follows the LIFO (Last In First Out) principle. You can visualize it like a stack of plates. The plate that was put on the stack last (at the top) is the first one to be removed.

In a stack, two primary operations are performed: 

- **push:** Adds an item to the top of the stack
- **pop:** Removes an item from the top of the stack

Here's a simple example of a Stack in JavaScript:

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  // Push operation
  push(element) {
    this.items.push(element);
  }

  // Pop operation
  pop() {
    if (this.items.length == 0) 
      return "Underflow"; // If stack is empty
    return this.items.pop();
  }

  // View the top of the stack
  peek() {
    return this.items[this.items.length - 1];
  }

  // Check if the stack is empty
  isEmpty() {
    return this.items.length == 0;
  }
}

let stack = new Stack();
stack.push(10);
stack.push(20);
console.log(stack.pop()); // Outputs 20
console.log(stack.peek()); // Outputs 10
```

**Queue**

A queue is another linear data structure that follows the FIFO (First In First Out) principle. You can visualize it like a queue of people. The person who was added to the queue first is the first one to be removed.

The two primary operations performed on a queue are:

- **enqueue:** Adds an item to the end of the queue
- **dequeue:** Removes an item from the front of the queue

Here's a simple example of a Queue in JavaScript:

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  // Enqueue operation
  enqueue(element) {
    this.items.push(element);
  }

  // Dequeue operation
  dequeue() {
    if(this.isEmpty()) 
      return "Underflow"; // If queue is empty
    return this.items.shift();
  }

  // View the front of the queue
  front() {
    if(this.isEmpty())
      return "No elements in Queue";
    return this.items[0];
  }

  // Check if the queue is empty
  isEmpty() {
    return this.items.length == 0;
  }
}

let queue = new Queue();
queue.enqueue(10);
queue.enqueue(20);
console.log(queue.dequeue()); // Outputs 10
console.log(queue.front()); // Outputs 20
```

These two structures are fundamental in computer science and used in numerous algorithms. They are especially important in breadth-first search and depth-first search of a graph, where queue and stack respectively are used to hold nodes to be processed.

## Recursion

 **Recursion**. 

Recursion in programming is a method where the solution to a problem depends on solutions to smaller instances of the same problem. It involves a function calling itself while a condition is met.

The basic idea behind recursion consists of the base case and the recursive case:

1. **Base Case:** The condition when the recursion ends. This is very important, as it stops the function from calling itself indefinitely.
2. **Recursive Case:** The part of the function that continues the recursion, usually with a different argument.

Here's a simple example of a recursive function in JavaScript that calculates the factorial of a number:

```javascript
function factorial(n) {
  // Base case
  if (n === 0) {
    return 1;
  }
  // Recursive case
  else {
    return n * factorial(n - 1);
  }
}

console.log(factorial(5));  // Output: 120
```
In the above example, `factorial(n - 1)` is the recursive case and `if (n === 0)` is the base case.

One common usage of recursion in data structures is for traversing trees or graphs.

Here's a quick example of how recursion can be used to sum an array:

```javascript
function sumArray(arr, index = 0) {
  // Base case: We've gone through every item in the array
  if (index === arr.length) {
    return 0;
  }
  // Recursive case
  else {
    return arr[index] + sumArray(arr, index + 1);
  }
}

console.log(sumArray([1, 2, 3, 4, 5])); // Outputs: 15
```

In this example, the function `sumArray` takes in an array and an index. In each recursive call, it adds the current index's value to the result of the rest of the array (obtained via a recursive call).

**Important Note:** While recursion can simplify several programming problems, keep in mind that each recursive call consumes memory for storing variables and parameters in the call stack. For deep recursion or recursion with a large input, you may encounter a stack overflow error. Therefore, for such situations, it may be better to use an iterative solution if possible.

**Iterative Solutions**. Iteration involves the use of loops (like for, while, do-while) to repeatedly execute a block of code.

Many problems that can be solved using recursion can also be solved using iteration. While recursion can make some problems easier to understand, iteration can often be more efficient as it doesn't require additional function calls and doesn't use additional space on the call stack.

Let's take the examples we used for recursion and see how they can be implemented iteratively:

1. **Factorial**

Here's how you would implement a factorial function using a for loop:

```javascript
function factorial(n) {
  let result = 1;
  for(let i = 1; i <= n; i++) {
    result *= i;
  }
  return result;
}

console.log(factorial(5));  // Output: 120
```

In this example, instead of making recursive calls, we use a loop that multiplies the `result` variable by each number from `1` to `n`.

2. **Sum of Array**

Here's how you would sum the elements of an array using a for loop:

```javascript
function sumArray(arr) {
  let sum = 0;
  for(let i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
}

console.log(sumArray([1, 2, 3, 4, 5])); // Outputs: 15
```

Here, we iterate through the array adding each element to the `sum` variable. This avoids the need for additional recursive function calls.

These are basic examples of how iteration can replace recursion. But remember, each approach has its pros and cons. Recursion can make code easier to write and read by expressing the problem in a clear and intuitive manner. Iteration, on the other hand, can be more efficient in terms of memory and performance.

Always consider the nature and size of the problem, the specific requirements you're facing, and the trade-offs between readability and performance when deciding which approach to use.
