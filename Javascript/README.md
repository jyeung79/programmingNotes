# Javascript-cheatsheet
Cheatsheet on Javascript language, programming paradigms, tips&tricks, etc. 

# Table-of-Contents
1. [What is Javascript]()
2. [Client-side vs Server-side](##client-side-vs.-server-side)
3. [Types of Front-End Frameworks]()
4. [JS Data Types](##4.-javascript-data-types)

[Academind Tricky Pasts](https://academind.com/learn/javascript/tricky-parts/)
1. Datatypes
2. Hoisting
3. Immutable Primitive & Reference values
4. Callbacks
5. Promises
6. this
7. Prototypes
	Fallback object
	```javascript
	Person.prototype = human; // Assigns all future instances of the object with protoype human 
	const max = new Person('max'); // Person's prototype does not change from Object or Function 
	```

## Prototypes
All objects have a prototype. A prototype is the base class that the object accesses all its prototype's methods & properties.

When defining functions for an object, it is better to do it on the ```prototype``` of that object. This is because defining the function in the constructor means that each time a new Object is created, the function gets duplicated.

```javascript
function Student(name) {
  this.name = name
  this.grade = grade
}

Student.prototype.sayName = function() {
  console.log(this.name)
}
Student.prototype.goToProm = function() {
  // eh.. go to prom?
}
```

Theres a method to setting the prototype of an object ```Object.create```. It returns a new object with the specified prototypes and any additional properties you want to add.

## 1. What is Javascript
Javascript is an interpreted language so it is interpreted line-by-line at run-time. Many browsers nowadays have Just-In-Time (JIT) compiliation which compiles Javascript into executable bytecode. This contrasts to compiled language such as C++, Java and Rust which must be compiled to machine code first before it's run.

## 2. Client-side vs Server-side
Javascript is a high-level programming language that focuses on running client-side code on the web browser. Client-side means that the code runs through the browser on the client or user's device when they open the website or such. This contrast to server-side which means that the action takes place on the web server instead of a user's computer.

 Javascript can do the following on the client-side such as.
<ol>
	<li> <strong>Render</strong> - Change the display or view on the browser
	<li> <strong>Post</strong> - Send data to a server
	<li> <strong>Get</strong> - Fetch more data from the server 
</ol>
However, with the advent of NodeJS, JS can be written on the server-side which means that it can now
<ol>
	<li> Write to APIs
	<li> Talk to Databases
	<li> Talk to Servers
</ol>

## 3. Front-End Frameworks
Front-end frameworks such as React, Angular and Vue enable client-side code to be easier and maintainable. There are strengths and caveats to each of the frameworks depending on usecases, project complexity and size etc.

## 4. Javascript Data Types
Javascript is a loosely typed or dynamic language. This means that variables are not directly declared it's typing compared to staticly typed languages such as C++. However, Typescript address this issues.

Data Types are split into two categories: Primitives or single celled data types and Objects or a group of data. Primitives are immmutable so variables can only be reassigned data.
Primitives include
<ol>
  <li> <strong>Boolean</strong> - true or false / 1 or 0
  <li> <strong>Null</strong> - user-assigned data type that says data has no value
  <li> <strong>Undefined</strong> - no datatype has been assigned to the variable or data is empty
  <li> <strong>Number</strong> - JS has number type as float data-types. This includes +/- infinity and NaN. BigInt can represent intergers beyond the safe integer limit for Nubmers with arbitrary preision. 
  <li> <strong>String</strong> - sequence of characters with indices
  <li> <strong>Symbol</strong> - unique and immutable primitive type and can be used as a key for an Object
</ol>
Objects include Arrays and Objects or commonly known as Hash Tables. 
Arrays are instatiated using [] and Objects are declared using {}.
Each array value has an index and a value. Each object has a key and a value.

```javascript
const fruits = ['bananas', 'tomatoes', 'apples', 1243.5545, null, true]; // Arrays can hold different primitives and object types
let trivia = {basketball:'Michael Jordan', hockey:'Wayne Gretzky', football:{ 1:45, 5:twenty, 8:566 running: function() } }; // Have objects nested into objects
```
Declare your variables with either const or let. Var can cause variables to leek out of it's block scope into outer scope. This can cause unpredictable and undesirable behavior.
```javascript
var i = 'happy'; // Don't use. Value escapes out of block scope. Deprecated use
const j = 12345; // Used to declare a variable and assign a value once. Cannot reassign new data
let k = []; // Declare a variable with reassignable values.
```

### 4.1 Array Methods

Javascript has a couple array methods that can alter the elements of an array.

1. ```pop()``` - Remove the last element of an array
2. ```push()``` - Add an item to the end of the array
3. ```shift()``` - Remove the first element of an array
4. ```unshift()``` - Add an item to the beginning of an array


## 5. Advanced Javascript



### 5.1. Promises vs Async/Await
Promise is an object that is a placeholder for the resulting value of an asynchronous operation. A promise is in one of these states:
<ul>
  <li> Pending: initial state neither fulfilled or rejected
  <li> Fulfilled: operation completed successfully
  <li> Rejected: meaning that the operation failed
</ul>
To understand Async/Await better you must understand <a href="https://medium.com/@bluepnume/learn-about-promises-before-you-start-using-async-await-eb148164a9c8"> promises.</a>
The reason you want to want to use Async/Await instead of Promises is to avoid
<a href="https://getstream.io/blog/javascript-promises-and-why-async-await-wins-the-battle/#callback-hell">Callback-hell.</a>

```javascript
function getUsers(userId) {
	axios
		.get(`/users/userId=${users[0]}`)
		.then(res => {
			// save the response for user 1
			response.push(res);

			axios
				.get(`/users/userId=${users[1]}`)
				.then(res => {
					// save the response for user 2
					response.push(res);

					axios
						.get(`/users/userId=${users[2]}`)
						.then(res => {
							// save the response for user 3
							response.push(2);

							axios
								.get(`/users/userId=${users[3]}`)
								.then(res => {
									// save the response for user 4
									response.push(res);
								})
								.catch(err => {
									// handle error
									console.log(err);
								});
						})
						.catch(err => {
							// handle error
							console.log(err);
						});
				})
				.catch(err => {
					// handle error
					console.log(err);
				});
		})
		.catch(err => {
			// handle error
			console.log(err);
		});
}
```

Instead you can use 
<a href='https://blog.logrocket.com/promise-chaining-is-dead-long-live-async-await-445897870abc/'>Async/Await</a>.
 Code is simplified and reduced significantly. Also there is no need to chain promises to make infinite callback loops.

```javascript
async function getUsers(users) {
	try {
		response[0] = await axios.get(`/users/userId=${users[0]}`);
		response[1] = await axios.get(`/users/userId=${users[1]}`);
		response[2] = await axios.get(`/users/userId=${users[2]}`);
		response[3] = await axios.get(`/users/userId=${users[3]}`);
	} catch (err) {
		console.log(err);
	}
}
```
Await must be used within functions that are declared with async in front. ie)

```javascript
async function makeCoffee() {
    try {
    	let cupOfMojo = await promiseToMakeCoffee;
    } catch(err) {
    	console.log('Let me sleep more Zzzzz');
    }
  }
  
  let result = await promiseToMakeCoffee;
  console.log(result);
}
```
However, if you don't have to wait for your responses sequentially you can wrap all your await statements in a Promise.all() function. The whole point of the event
loop is to avoid blocking code.
```javascript
async function getUsers(users) {
	try {
		user0 = axios.get(`/users/userId=${users[0]}`);
		user1 = axios.get(`/users/userId=${users[1]}`);
		user2 = axios.get(`/users/userId=${users[2]}`);
		user3 = axios.get(`/users/userId=${users[3]}`);

		response = await Promise.all([user0, user1, user2, user3]);
	} catch (err) {
		console.log(err);
	}
}
```
<ol>
  <li> Async/Await reduces the amount of code and cleans it up without complicated, nested promises
  <li> Can use error handling with try/catch instead of in each promise
  <li> Error stacks shows exact place instead of ambiguous errors in Promises loops
  <li> Avoid Callback-hell (Not fun :sob: )
</ol>

### 5.2. Scope vs Context
Scope refers to the visibility of the variables while context refers to the object to which a function belongs.
http://ryanmorr.com/understanding-scope-and-context-in-javascript/

<dl>
	<dt>Scope</dt>
	<dd>Scope pertains to the variable access of a function when it is invoked and is unique to each
	invocation.</dd>
	<dd>Var is function scoped and let is block scoped which is denoted by the enclosing block {}.</dd>
	<dt>Context</dt>
	<dd>Is always the value of ```this``` keyword which is a reference to the object
	that "owns" the currently executing code.</dd>
	<dd>Using 'this' keyword refers to the object that the function is executing in.</dd>
</dl>

```javascript
	var shop = {
	fruit: "Apple",
	sellMe: function() {
		console.log("this ", this.fruit);
	// => this Apple
		console.log("shop ", shop.fruit);
	// => shop Apple
	}
}

shop.sellMe()
```

Window Scope : if you declare a and b on your browser then you will see the a and b in your window
Global Scope: variables declared in the global scope can be accessed anywhere in the file
	- global to the file or global relative to some block of code (block scope)
Local Scope: Local scope means it can be accessed only in a certain block of code



https://medium.com/dev-bits/a-perfect-guide-for-cracking-a-javascript-interview-a-developers-perspective-23a5c0fa4d0d
There are three types of scopes in ES6.
<ul>
	<li>Global scope: Variables declared in the global scope can be accessed by all functions.</li>
	<li>Local Scope/Function Scope: Variables declared can only be accessed within 
	the function itself.</li>
	<li>Block scope(ES6): Variables declared can only be accessed within the block {} scope.</li>
</ul>


### 5.1.3. Closures
Closures are when a nested or inner function declared inside an outer function has access to the outer functions variables. To expose a function, return it or pass it to another function to use the closure.

https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36

This is similar to the getter or setter functions of a class object in C++. 

### Arrow functions
Arrow functions make writing functions compact and removes issues with the ```this``` keyword. The context for this will not change during run-time. However they are ill suited as methods and cannot be used as constructors.

```javascript
// Regular function expression
function fryHamburger(ingredients) {
	//frying hamburger
}
// Arrow function expression for no args
const fryHamburger = () => {
	//frying hamburger
};
// One argument arrow function expression
const fryHamburger = patties => {};
// Multiple argument arrow function
const fryHamburger = (buns, patties, lettuce) => {};
// Write in one line
const fryHamburger = (buns, patties, lettuce) => console.log("Hamburger is done");
```
### Exports & Imports
Divide your javascript code across multiple files using export/import

```javascript
// export default means if you import the object it will provide this default object
export default person = {name:"Max"};
export cleaner = () => {...};
export function findCops(args) {...}

import person from './person.js';
// rename the import object name
import prs from './person.js';

// If you want to specify named imports
import { smth } from './utility.js';
import { smth as Smth } from '.utility.js';
// Can import all functions/object into one object
import * as bundled from 'utility.js';
```

### Classes & Inheritance
Classes are prototypical inheritance model that you call to create an object of a certian blueprint. This is comparable to classes in other programmming languages such as C.

```javascript
class Human {
	constructor() {
		this.gender = "male";
	}

	printGender() {
		console.log(this.gender);
	}
}

class Person extends Human {
	constructor() {
		super(); // Super allows your derived class to use the properties/methods of the inherited class
		this.name = "max";
		this.gender = "female";
	}

	printName() {
		console.log(this.gender);
	}
}
```

### Spread & Rest Operators
```...``` can be used as a spread or a rest operator.
<dl>
	<dt>Spread</dt>
	<dd>Used to split up array elements or Object properties</dd>
	<dd>Pulls out the elements out of the array or key pairs out of objects</dd>
</dl>	

```javascript
const newArray = [...oldArray, 1, 2];
const newObject = {..oldObject, newProp:5};
```

<dl>
	<dt>Rest</dt>
	<dd>Used to merge a list of function arguments into an array</dd>
</dl>

```javascript
function sortArgs(...args) {
	return args.sort();
}
```

### Destructuring



### Higher Order Functions

Higher order functions take other functions as a parameter or return a function as a value. The function passed
as a parameter is called callback.

#### Callback

A callback is a function which can be passed as parameter to other functions.

```javascript
const mixBatter = (ingredients) => {
	// Mix ingredients
};

const makeCupcakes = (mixBatter, ingredients) => {
	return mixBatter(ingredients);
}

```

Understanding [callbacks](https://briggs.dev/blog/understanding-callbacks)

Q: How does a promise work then? How is callback hell related to functions?

#### Returning functions

Higher order functions return functions as values.

```javascript
// Higher order function returning an other function
const higherOrder = n => {
  const doSomething = m => {
    const doWhatEver = t => {
      return 2 * n + 3 * m + t
    }
    return doWhatEver
  }
​
  return doSomething
}
console.log(higherOrder(2)(3)(10))
```

forEach, map, reduce all use callback functions to do some sort of function call

### Functional Programming

These built-in Array prototype functions all use callbacks functions.
ie) forEach, map, filter, reduce, find, every some, and sort

Callback function Methods
* forEach: Iterates through the array's elements and applies a callback function to each element
* map: Returns a new array with a callback function applied to the input array
* filter: Return the items that fulfill the filtering conditions
* reduce: Returns a single accumulator value from sum and value
* every: Returns boolean from checking if all elements meet the same condition
* find: Return first element that meets the condition
* findIndex: Return index of first element that meets condition
* some: Check if one or more elements meet the condition
* sort: Modifies the original array and sorts it by ascending or descending order
  * Note: sort() for numbers sorts it as strings not numbers. Refer to fix below

```javascript
const numbers = [9.81, 3.14, 100, 37]
console.log(numbers.sort()) //[100, 3.14, 37, 9.81]
numbers.sort(function(a, b) {
  return a - b
})

console.log(numbers) // [3.14, 9.81, 37, 100]

numbers.sort(function(a, b) {
  return b - a
})
```

### Sets & Maps

#### Sets

Set is a collection of elements. Compared to arrays, a set can only contain unique elements.

```javascript
const companies = new Set(); // {} Sets are also objects

const fruit = ['apples', 'oranges', 'apples', 'bananas'];
const fruitNames = new Set(fruit); //Set(4) {'apples', 'oranges', 'bananas'}
```

Sets can be used to:

1. Count unique items in an array
2. Find a union of two sets
3. Difference of two sets

```javascript
//Union of sets
let a = [1, 2, 3, 4, 5]
let b = [3, 4, 5, 6]
let c = [...a, ...b]

let A = new Set(a)
let B = new Set(b)
let C = new Set(c) // Set(6) {1, 2, 3, 4, 5, 6}

//Intersection of Sets
let a = [1, 2, 3, 4, 5]
let b = [3, 4, 5, 6]

let A = new Set(a)
let B = new Set(b)

let c = a.filter(num => B.has(num))
let C = new Set(c) // Set(3) {3, 4, 5}

// Difference of Sets
let a = [1, 2, 3, 4, 5]
let b = [3, 4, 5, 6]

let A = new Set(a)
let B = new Set(b)

let c = a.filter(num => !B.has(num))
let C = new Set(c) // Set(2) {1, 2}

```

#### Maps




### [Function Declaration vs Expression](https://medium.com/@mandeep1012/function-declarations-vs-function-expressions-b43646042052)

Function declaration means that the function is "saved for later use" while function expressions
are executed when the interpreter reaches that line of code.

```javascript
// Function Expression
console.log(foo()); // ERROR foo wasn't loaded
const foo = function { return 'foo'; }

// Function Declaration
console.log(boo()) // Prints 'boo' onto console
const function boo() { return 'boo'; }
```

Function declarations are hoisted to the top of the code while function expressions are not.
Benefits of using function expressions are:

1. Closures
2. Arguments to other functions
3. IIFE

NOTE: Arrow functions are similar to function expressions so they are not hoisted.

### [IIFE](https://flaviocopes.com/javascript-iife/)

Immediately invoked function expressions are immediately called when they are defined. 

```javascript
(/* function declaraction - function declaration or arrow function */) ();
(() => {
	/* Arrow function for anonymous function */
})())


// IIFE can be named but they do not leak out to the global scope
(function doSomething() {
	/* Function is doing something */
})())

```

Benefits of using IIFE

1. Avoid polluting global object
2. Isolate variables declaration
