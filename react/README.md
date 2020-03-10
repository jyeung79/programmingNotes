# ReactJS Cheatsheet
React is a front-end framework that simplifies the difficulty of implementing web apps by making it declarative and component based.

The three main principles of React are
<ol>
    <li> **Declarative** - Have different views for different states of your applications. The views will update and render when the VDOM and DOM have differences. This makes code more predictable, simpler to understand and easier to debug.
    <li> **Componenents** - Escapsulated components that manages its own state meaning there's separation of responsibility and that the component does not affect the views or state.
    <li> **LO,WA** Develop new features in React without rewriting previous code. Backwards-compatible.
</ol>

## JSX
React uses JSX which is a subset of Javascript that allows writing of HTML directly within Javascript code. Thus it means that you are able to incorporate HTML tags or such into Javascript. 
```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
    <div className='Header' datatest-id='Header'>
        <h1>
            Hello, {formatName(user)}!
        </h1>
    </div>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

## Components
Components are encapsulated parts of code that can be resusable and isolated. This means you can modify the componenents without changing other files or functions.
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

## States
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
 
 
Use states (this.state) to manage dynamic data.

With Babel you can use proposal-class-fields and get rid of constructor

class Hello extends Component {
  state = { username: undefined };
  ...
```

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

https://reactjs.org/docs/hello-world.html
https://devhints.io/react