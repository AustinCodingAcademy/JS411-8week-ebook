# Component Lifecycle

*Let us make our future now, and let us make our dreams tomorrow’s reality. —Malala Yousafzai*

We've done a lot in the past two weeks getting up to speed with React but there are some deeper level concepts we need to cover and firmly grasp. Today we will take a deeper dive into React's Class-Based Component Lifecycle and the methods involved, but before we do let's look at this JSX syntax a little more closely. 

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-25-JSX:Why? - 411.2.2.1 -->
<iframe src="https://player.vimeo.com/video/492186665?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Overview

The **Component Lifecycle** is a set of steps that every class-based component goes through from when the component is referenced/invoked and mounted in the DOM to when it is closed out and removed from the DOM, birth to death. This  *Lifecycle* can be divided into 4 phases: **Mounting**, **Updating**, **Unmounting**, & **Error**. Inside of each of these phases are individual methods(properties with functions as their definition/value). These methods are appropriately classified as **lifecycle methods** because they get called throughout each phase and each has a purpose... we will get into soon.

### Why?

*The purpose of these lifecycle methods is to capture or encapsulate the manipulation, moving, and rendering of data inside of each component, just like JSX provides easier syntax for doing this.* Having the ability to pinpoint certain points of execution during a component's "life" gives us greater flexibility, programming customization, and testing opportunities. For example, we may want to load some data into our component before we render it onto the screen. It just so happens that there is a lifecycle method called `componentDidMount` that fires after the initial `render` method. This is a great place to make a call for that data. And yes, `render()` is a lifecycle method too. If your data hasn't come back from the API yet you might offer the user a spinning wheel or cute animation through the use of conditional rendering in your render statement so when your data does come in, you can call render again.

These methods become more and more useful as you grow into your new trade and become more proficient. For now, let's cover the most commonly used methods and how to mentally model what they are and how to use them.

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-26-LifecycleMethods-Why&What - 411.2.2.2 -->
<iframe src="https://player.vimeo.com/video/492195162?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Read It - Class-Based Component Lifecycle

We've talked briefly about what the component lifecycle is and why it's useful so let's get a little more into the details of the operation. I'd like to start with how these lifecycle methods are accessed.

From the past couple classes, you've likely become familiar with seeing a component written like this:

=== "Two ways to extend Component"

    ```javascript
    import React from 'react'

    class MyComponent extends React.Component {
        render() {
            return (
                <div>
                    <h1>Welcome to our component</p>
                </div>
            )
        }
    }
    // Or...

    import React, { Component } from 'react'

    class MyComponent extends Component {
        render() {
            return (
                <div>
                    <h1>Welcome to our component</p>
                </div>
            )
        }
    }
    ```

The above two examples are the exact same in terms of functionality. The only difference is that we imported Component separately in the second example. Let's talk about that a little.

The reason we have access to any of these methods (for example: `render`) is because of the "Component" keyword on line 1 and/or 3 of the two examples above. When we create our component with `class MyComponent`... and use `extends Component`, which we've imported from `React`, we are saying (in code) that we want our class to have all the capabilities of a React class component (a class that is built into the React node module). The method `render` actually lives on that `Component` and the only reason we get to use it is that we "extended" from `Component` with a class of our own. Fortunately for us, `Component` has a few other useful methods to use the same way:

*****

### The `componentDidMount` Method

This method, when used in your component, fires when the component is inserted into the DOM tree. This happens after the initial "render" method and can be useful for fetching data or updating state based on some conditions. The `componentDidMount` method (and other lifecycle methods) are usually placed above the `render` method. Here's an example:

=== "Example of componentDidMount"

    ```javascript
    import React, { Component } from 'react'

    class MyComponent extends Component {
        constructor() {
            this.state = {
                data: []
                }
        }
        componentDidMount() {
            fetch('http://example.com')
                .then(res => res.json())
                .then(examples => {
                    this.setState({ data: examples })
                })
        }

        render() {
            return (
                <div>
                    <h1>Welcome to our component</p>
                    <p>Take a look at our data: {this.state.data}</p>
                </div>
            )
        }
    }
    ```
=== "Functional version with hooks"

    ```javascript
    import React, { useState, useEffect } from 'react'

    function MyComponent() {
        const [data, setData] = useState([]);
        
        useEffect(() => {
            fetch('http://example.com')
                .then(res => res.json())
                .then(examples => {
                    setData(examples)
                })
        }, []); // empty dependency array so it will only run when first mounting

            return (
                <div>
                    <h1>Welcome to our component</p>
                    <p>Take a look at our data: {data}</p>
                </div>
            )
    }
    ```

*****

#### The `render` Method

This may seem redundant but the `render` method is important to understand since it is the only *required* method when using a class component. The `render` method typically returns JSX but it can also return other things, namely:

* Arrays
* Strings/Numbers
* Booleans
* Null

The above options aren't typical so we will focus on JSX. It's also important to note that the render method should be a "pure function" which means it **doesn't update state**. The second rule to render is that it **must return something**...JSX, `null`, an array, whatever. It must return something.

Speaking of state, we need to remember that this render method will be invoked each time the state changes. Calling `this.setState()` anywhere in your component will cause this function to fire again and update the parts of the DOM that may have changed.

In the following code, how many times will the render method be called on initiation?

=== "Simple Class Component"

    ```javascript
    import React, { Component } from 'react'

    class MyComponent extends Component {
        constructor() {
          this.state = {
              users: []
            }
        }

        componentDidMount() {
            const arr = this.props.users.filter(u => u.username.length > 5)
            this.setState({ users: arr })
        }

        handleClick = () => {
            this.setState({ users: [...this.state.users].concat(['newUser']) })
        }

        render() {
            return (
                <div>
                    <h1>Welcome to our component</p>
                    <p>Here's an array with our users: {this.state.users}</p>
                    <button onClick={this.handleClick}>Add User</button>
                </div>
            )
        }
    }
    ```
=== "Functional version with hooks"

    ```javascript
    import React, { useState,useEffect } from 'react'

    function MyComponent(props) {
        const [users, setusers] = useState([]);
        const propUsers = props.users;
	 
        useEffect(() => {
           const arr = propUsers.filter(u => u.username.length > 5)
            setusers(arr)
        }, [propUsers]); // any props used inside this useEffect must go in the dependency array
            
        const handleClick = () => {
             setusers([...users].concat(['newUser']))
        }
        
        return (
            <div>
                <h1>Welcome to our component</h1>
                {errText && <p>{errText}</p>}
                <p>Here's an array with our users: {users}</p>
                <button onClick={handleClick}>Add User</button>
            </div>
        )
    }
    ```



The key is in the word *"initially"*. Hopefully you guessed 2 times. The render will be invoked a third time when the button is clicked.

The answer is two because `this.setState` is asynchronous and the initial render will attempt before the `componentDidMount` function is complete. However, `componentDidMount` will quickly update the state and re-render the component without the user noticing anything. You can read more about that process in the [React Docs](https://reactjs.org/docs/react-component.html#componentdidmount).

Before we move to another lifecycle method let's remember that everything is an object including this React component we're extending. What this means is that it too has properties, or methods(because their values are functions). Just like all of the methods on the DOM or any HTML element you've worked with like onclick, hover, blur...etc, this React Component has method that are firing blanks throughout the cycles of its life until YOU, the developer, give them instructions. Here's invalid code but a good visual example of what the Component you're extending looks like under-the-hood.

=== "Under-the-hood look at the lifecycle methods - Invalid Code!"

    ```javascript
    // * React Class Component /Object-Thing/
    myComponent = { 

      constructor: () => {/* create state here */},

      componentDidMount: () => {/* fetch data here */}, 

      componentDidUpdate: () => {}, 

      componentWillUnmount: () => {/* delete cookies, unsubscribe from current connections, sign out here */},

      render: () => {/* return the visual for the DOM in JSX here */},

      componentDidCatch: () => {/* process error handling here */},

      getDerivedStateFromError: () => {},

      shouldComponentUpdate: () => {},

      getSnapshotBeforeUpdate: () => {},

      getDerivedStateFromProps: () => {},

    }

    ```

Now that you see each property is already declared on the class, you can now go and define them with whatever your application's needs are! If you don't need them, don't worry about them they'll just fire blanks with no side-effects!

*****

#### The `componentDidUpdate` Method

This method is called when the component is updated. What does "updated" mean? It means when `this.setState` is called somewhere in the tree that affects the current component. This lifecycle method is not called on the initial load of the component. When it is called it automatically gives us a variable called `prevProps` that we can use to see if any of the props changed. You can call `this.setState` in this function but you want to be careful to do it based on some condition. If you don't, you'll cause an infinite loop because `setState` will cause the component to "update" which will then call `setState` which will cause it to update again, etc, etc, etc. For this reason, this is 

=== "Example of componentDidUpdate"

    ```javascript
    componentDidUpdate(prevProps, prevState, snapshot) {

      // will not be invoked if shouldComponentUpdate() returns false.

      // Use to do side effects if the state or props change and those create a need for a side-effect like a data fetch/network request or visuals

      // fired every time render is called after the initial render call

      // If we have a snapshot value, we've just added new items.

      // Adjust scroll so these new items don't push the old ones out of view.

      // (snapshot here is the value returned from getSnapshotBeforeUpdate)



      if (snapshot !== null) {

        const list = this.listRef.current;

        list.scrollTop = list.scrollHeight - snapshot;

      }
    }
    ```

=== "Example of componentDidUpdate"

    ```javascript
    // this.setState({}) ->
      // componentDidUpdate() ->
    // this.setState({})->
      // componentDidUpdate() ->
    // this.setState({})->
      // etc.
    // This lifecycle method can be used like this:

    import React, { Component } from 'react'

    class MyComponent extends Component {
        constructor() {
          this.state = {
              users: [],
              errText: ""
            }
        }

        componentDidUpdate() {
            if (this.state.users.length === 0) {
                this.setState({ errText: 'There are no users to show' })
            }
        }

        handleClick = () => {
            // This line is a shorthand to set the state to equal what the list of users was plus the new user that was added.
            this.setState({ users: [...this.state.users].concat(['newUser']) })
        }

        render() {
            return (
                <div>
                    <h1>Welcome to our component</h1>
                    {this.state.errText && <p>{this.state.errText}</p>}
                    <p>Here's an array with our users: {this.state.users}</p>
                    <button onClick={this.handleClick}>Add User</button>
                </div>
            )
        }
    }
    ```
=== "Functional version with hooks"

    ```javascript
    import React, { useState,useEffect } from 'react'

    function MyComponent() {
        const [users, setusers] = useState([]);
	    const [errText, setErrText] = useState('');
	 
        useEffect(() => {
            if (users.length === 0) {
                setErrText('There are no users to show' )
            }
        }, [users]); 
            
        const handleClick = () => {
            setusers([...users].concat(['newUser']))
        }
        
        return (
            <div>
                <h1>Welcome to our component</h1>
                {errText && <p>{errText}</p>}
                <p>Here's an array with our users: {users}</p>
                <button onClick={handleClick}>Add User</button>
            </div>
        )
    }
    ```


*****

#### The `constructor` Method

The `constructor` is the first thing that happens when you load up a component. In fact, it's the first thing that happens anytime you use a class in JavaScript for any purpose (not just React). Inside the constructor is where you initialize variables that your class, or component, will use. For example, this is where you typically set your initial state. You also call the `super()` function inside of the constructor. This function calls the parent constructor with the data you've passed in, but we don't need to know about the details of that here so let's take a look at how we use the constructor:

=== "Example Usage of constructor"

    ```javascript
    import React, { Component } from 'react'

    class MyComponent extends Component {
        constructor() {
            super() // calls the functionality of the grandparent class(the class parent of the Component class)
            this.state = {
                count: 0
            }
        }

        handleClick = () => {
            this.setState({ count: this.state.count + 1 })
        }

        render() {
            return (
                <div>
                    <p>The count is: {this.state.count}</p>
                    <button onClick={this.handleClick}>Add 1</button>
                </div>
            )
        }
    }
    ```

It's important to note that many people have stopped using the constructor in such verbose terms since React released shortcuts for writing this. Essentially, it does the same thing behind the scenes but the above can now also be written as:

=== "State without calling constructor"

    ```javascript
    import React, { Component } from 'react'

    class MyComponent extends Component {
        state = {
            count: 0
        }

        handleClick = () => {
            this.setState({ count: this.state.count + 1 })
        }

        render() {
            return (
                <div>
                    <p>The count is: {this.state.count}</p>
                    <button onClick={this.handleClick}>Add 1</button>
                </div>
            )
        }
    }
    ```

*****

### Order of Operations

The lifecycle methods we just covered were not in any specific order so below we'll order them by the way they fire when the component is **mounted**, **rendered**, **updated**, **unmounted**, and if an **error** occurs. These phases are the phases of the components cycle of life, a.k.a the order in which the methods are fired as the component comes into the DOM(mounts) and eventually leaves the DOM (unmounts).

#### Mounting Phase

* **constructor()**
* **render()**

#### Updating Phase

* **shouldComponentUpdate(nextProps, nextState)**
* **render()**
* **componentDidUpdate(prevProps, prevState, snapshot)**
* **getSnapshotBeforeUpdate(prevProps, prevState)**
* **static getDerivedStateFromProps(props, state)**

#### Unmounting Phase

* **componentWillUnmount()** - used to fire before the render method but it is now considered legacy and unsafe to use.

#### Error Phase - Not used to handle exceptions!

* **componentDidCatch()**
* **getDerivedStateFromError()**

A full, [comprehensive breakdown of all lifecycle methods can be found in here](https://blog.logrocket.com/the-new-react-lifecycle-methods-in-plain-approachable-language-61a2105859f3/). We encourage you to look at this page often as well as use this [lifecycle cheatsheet](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/) as you develop.

Other component lifecycle methods and properties you should become familiar with are:

* **setState()**
* **forceUpdate()**
* **defaultProps**
* **displayName**

## Summary

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-27-LifecycleMethod-HighOverview - 411.2.2.3 -->
<iframe src="https://player.vimeo.com/video/492200585?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Practice It

Work through the [React Docs Tutorial](https://reactjs.org/docs/state-and-lifecycle.html) to build a timer app that utilizes the lifecycle methods.

## Additional Resources

- [ ] [Blog, CodeBurst - How to Use the Lifecycle Methods](https://codeburst.io/how-to-use-react-lifecycle-methods-ddc79699b34e)
- [ ] [Blog, Blog - React Component Lifecycle](https://medium.com/react-ecosystem/react-components-lifecycle-ce09239010df)
- [ ] [Reference, Wojtekma - Lifecycle Methods Diagram](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
- [ ] [Reference, LogRocket - The New React Lifecycle Methods](https://blog.logrocket.com/the-new-react-lifecycle-methods-in-plain-approachable-language-61a2105859f3/)

## Know Your Docs

- [ ] [React Docs - componentDidMount](https://reactjs.org/docs/react-component.html#componentdidmount)
- [ ] [React Docs - React Component](https://reactjs.org/docs/react-component.html)
