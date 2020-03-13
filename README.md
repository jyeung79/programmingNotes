# Javascript-cheatsheet
Cheatsheet on Javascript language, programming paradigms, tips&tricks, etc. 

Javascript is an interpreted language so it is interpreted line-by-line at run-time. Many browsers nowadays have Just-In-Time (JIT) compiliation which compiles Javascript into executable bytecode. This contrasts to compiled language such as C++, Java and Rust which must be compiled to machine code first before it's run.

## Client-side vs Server-side
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

### Front-End Frameworks
Front-end frameworks such as React, Angular and Vue enable client-side code to be easier and maintainable. There are strengths and caveats to each of the frameworks depending on usecases, project complexity and size etc.

## OOP vs Functional programming
Object Oriented Programming - programming paradigm that focuses on three aspects
<ol>
  <li> Encapsulation - Hiding implementation details from outside to prevent improper changes to private data. ex) Black box with known inputs and outputs
  <li> Inheritance - Child classes derives attributes and methods from parent classes. Child classes may have uniqure attributes apart from parent class. This is the same as JS Object Prototypes. All JS objects inherit properties and methods from a prototype. ex) I inherit my big butt genes from my parents
   <li> Polymorphism - Objects can take on multiple forms. Methods that might belong to one class might be overridden with a diffrent implementation. This includes function/operator overloading and overriding. ex) A man can be a father, a husband, an employee and NBA basketball player
</ol>
<a href="https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0">Functional Programming</a> - a programming paradigm that focuses on pure functions
<ol>
  <li> Pure functions - functions where return values are only determined by input values without observable side effects
  <li> Function composition
  <li> No shared state
  <li> No side-effects
  <li> Immutable data
</ol>

### Javascript Data Types
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

### Promises vs Async/Await
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

### Scope vs Context
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
https://medium.com/dev-bits/a-perfect-guide-for-cracking-a-javascript-interview-a-developers-perspective-23a5c0fa4d0d
There are three types of scopes in ES6.
<ul>
	<li>Global scope: Variables declared in the global scope can be accessed by all functions.</li>
	<li>Local Scope/Function Scope: Variables declared can only be accessed within 
	the function itself.</li>
	<li>Block scope(ES6): Variables declared can only be accessed within the block {} scope.</li>
</li>

### Closures
Closures are when a nested or inner function declared inside an outer function has access to the outer functions variables. To expose a function, return it or pass it to another function to use the closure.

https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36

This is similar to the getter or setter functions of a class object in C++. 