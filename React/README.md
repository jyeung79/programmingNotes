# ReactJS Cheatsheet
React is a front-end framework that makes writing client-side code easier and more maintainable.

The three main principles of React are
<ol>
    <li> **Declarative** - Have different views for different states of your applications. The views will update and render when the VDOM and DOM have differences. This makes code more predictable, simpler to understand and easier to debug.
    <li> **Componenents** - Escapsulated components that manages its own state meaning there's separation of responsibility and that the component does not affect the views or state.
    <li> **LO,WA** Develop new features in React without rewriting previous code. Backwards-compatible.
</ol>

## 1. JSX
**JSX IS NOT HTML.** React uses JSX which is a subset of Javascript that allows writing of HTML directly within Javascript code. Thus it means that you are able to incorporate HTML tags or such into Javascript.


```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = ( 
  // JSX Code
    <div className='Header' datatest-id='Header'>
        <h1>
            Hello, {formatName(user)}!
        </h1>
    </div>
  // End of JSX
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

React calls ```React.createElement(...)``` when it parses the JSX code. Writing JSX is much easier and cleaner than calling ```React.createElements(...)``` over and over again.

## 2.Components
Components are encapsulated parts of code that can be resusable and isolated. This means you can modify the componenents without changing other files or functions.

Components can be written as a **class-based component**:

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
class Hello extends React.Component {
  render () {
    return <div className='message-box'>
      Hello {this.props.name}
    </div>
  }
}
const el = document.body
ReactDOM.render(<Hello name='John' />, el)
```

or can be written as a **Functional component**

```jsx
const Hello = (name) => (
    <div className='message-box'>
      Hello {name}
    </div>
);
const el = document.body
ReactDOM.render(<Hello name='John' />, el)
```

Only two things lead React to update the DOM: States & Props.


### 2.1. Props

You can pass in arguments to your components through ```props``` object arguments.

```jsx
// Hello Component files
const Hello = (props) => (
    <div className='message-box'>
      Hello {props.name}
    </div>
);
// Other file
<Hello name='Jennifer'/>
```

Another cool thing is passing the ```children``` argument. Following the above example we modify the Hello component.

```jsx
const Hello = (props) => (
  <div>
    Hello {props.name}
    {children}
  </div>
);

<Hello name='Rem'>Rem is the best!</Hello>
```

Anything that is passed between the opening and closing tag of the component is considered to be the ```children``` argument. Anything can be passed as the ```children```.


You can pass methods as props such as ```onClickHandler``` or other events by reference. 


### 2.2. Bind vs arrow function passing

Bind performance should be much better than arrow function performance. Depends on the size of the application, the performance hit of using arrow functions might not be as major.

https://medium.com/@charpeni/arrow-functions-in-class-properties-might-not-be-as-great-as-we-think-3b3551c440b1#:~:text=The%20initialization%20of%20arrow%20functions,are%20transpiled%20into%20the%20constructor.&text=them%20with%20super%20.-,Arrow%20functions%20in%20class%20properties%20are%20much%20slower%20than%20bound,going%20to%20pass%20it%20around

## 3. States
States are inner properties of the component that are seperate from the outer code and maintain it's state throughout it's lifecycle. 
```jsx
constructor(props) {
  super(props)
  this.state = { username: undefined }
}
this.setState({ username: 'rstacruz' })
render () {
  this.state.username
  const { username } = this.state
  ···
}
```
 
Use states (this.state) to manage dynamic data.

With Babel you can use proposal-class-fields and get rid of constructor

```jsx
class Hello extends Component {
  state = { username: undefined };
// ...rest of class

<Hello name={this.state.username} />
```

*HOWEVER,* there's a new way to maintain states called **Hooks**.  

Class-based components states only have 1 state but functional components have multiple ```useState()```.
Also, old states in functional states do not get merged compared to class-based components. However, in functional components you separate your states into multiple states instead.


### 3.1. Events

There is a list of supported events for React components:

https://reactjs.org/docs/events.html#supported-events

### 3.2. Manipulating States


### 3.3. Stateful vs Stateless Components


## Hooks
Hooks are a functions that allow you to use states and modify states without writing classes. They typically start with a *useState*, *useBurger* or *use...*. Hooks was released in React 16.8

```jsx
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
There are also effect hooks which runs additional code  or *"side effects"* after the DOM has been updated. These effects include data fetching, setting up a subscription and manually changing the DOM.
```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

# 4. Understanding The Base Features & Syntax

We need to
1. Dependency/Package manager tool (npm or yarn)
2. Bundler of files (webpack)
3. Compiler of next-gen features to older browsers (babel)


https://reactjs.org/docs/hello-world.html
https://devhints.io/react