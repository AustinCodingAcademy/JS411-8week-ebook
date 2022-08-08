# Functional Components with Hooks

*Trust the process.*

## Overview: Replace Class-based with Functional + Hooks

We've been learning React through Class-based Components but we're now going to switch them out for Functional components. And instead of using Lifecycle methods, we'll use things called Hooks.

That being said . . . why use React Hooks? Well . . . because it allows us to use things like `state` in our functional components. When we say "state" here we mean local component state. Not global app state created by Redux.

## React Hooks

What are Hooks? They are simple pieces of React code that were added in 2018, to great fanfare among React developers. As we mentioned above, they allow you to use "state" in functional components (*not class-based components*). This promotes code cleanliness, only pure functional components, as well, code performance. The best way to learn about it is to just dive right in so we will look at an example.

The following is an example taken directly from the [React website](https://reactjs.org/docs/hooks-intro.html). Take a look at it and see if you can identify what looks different about it than the other React components you've seen and built.

=== "Functional `ExampleComponent.js`"

    ```javascript
    import React, { useState } from 'react';

    function ExampleComponent() {
      // Declare a new state variable, which we'll call `count` with an initial value of `0`
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

    export default ExampleComponent
    ```

So what's happening in the component above? Well the first thing we notice is that we are importing the hook called `useState` from `React`. You can see that being used on the first line of the component. In fact, that's the only other line we need to talk about.

If you remember, you can declare two variables at once using [array destructuring](https://dev.to/sarah_chima/destructuring-assignment---arrays-16f) and that's exactly what's happening here with `[count, setCount]`. Count will represent the value of state you want to use. Using regular state, it would look like this:

=== "Class-Based `ExampleComponent.js` Equivalent"

    ```javascript
    import React, { Component } from 'react'
    
    class ExampleComponent extends React {
    constructor(props) {
        super(props)

        this.state = {
        count: 0
        }
    }

    setCount = () => {
        this.setState({
        count: count + 1
        })
    }

    render() {
        return (
        <div>
            <p>You clicked {this.state.count} times</p>
            <button onClick={this.setCount()}>
            Click me
            </button>
        </div>
        )
    }
    }

    export default ExampleComponent
    ```

You'll notice that we set the `count` equal to `0`. The way that happened with React Hooks was on the fifth line of the first snippet, which reads `useState(0)`. The `useState` function is called with the initial value you want to set to a variable, in this case, `count`. So there's only one part left and that's the `setCount` variable. That variable represents a function and you call it when you want to change that particular piece of state! If we wanted to change the `count` to `1` we would write `setCount(1)` somewhere in the component. You can see an example of this in the button's `onClick` method. `<button onClick={() => setCount(count + 1)}>`, line 10.

Pretty simple stuff right? There are other hooks like `useEffect` that exist but we won't dive into those right now. We simply wanted to bring this to your attention because we know that you'll encounter it on your path to becoming front-end developers. One main place that you'll see Hooks used is in the Material-UI documentation (coming up in a couple of class lessons). Typically, when an update as popular as this happens, people start integrating it as quickly as possible.

## Why Functional over Class-based

Why did we learn Class-based and now have to replace them? 

Class-based & Functional components have been part of React since React's inception, May 29, 2013. Accept back then, Class-based components were previously the **only** way to manage component state because you could create `this.state = {}` in a class. With the advent of Hooks, introduced in React v16.8, we can now manage component state in Functional components. Because of this new way of component state management, the memory efficiency of Functional components, less boilerplate code, and cleanliness of the code developers now favor Functional components with hooks when writing new code. This being said, legacy code-bases will have both and you'll need to know how to read and write each.   

Here is a scenario that demonstrates a use case for why developers favor functional components with hooks. Let's say last week you made this simple display component.

=== "Functional Component of `App.js`"

    ```javascript
    import React from 'react'

    function App() {
        return <h1>Simple Functional Component</h1>
    }
    ```

Now we've been asked to add some component state to toggle between `visible` and `hidden` statuses. Before hooks we would have to go through the process and convert it to a Class-based component then add a `constructor()`, `super()`, `this.state={}`, then create values to hold the state, plus passing in an object the the method...blah blah blah. With Hooks, we can keep our component as a Function by simply adding in one of the hooks, known as `useState` then handling the click with a custom build method:
       
=== "State management using the `useState` Hook of `App.js`"

    ```javascript
    import React, { useState} from 'react';

    function App() {
        const [isHidden, setIsHidden] = useState(false);

        const handleClick = () => {
            let status = isHidden === true ? false : true
            setIsHidden(status);
        }
        
        return (
            <div>
                <p>The Status of hidden is {`${isHidden}`}</p>
                <h1 onClick={handleClick}>Functional Component Using State</h1>
            </div>;
        )
    }
    ```

Above `useState()` is a hook (just a function) imported from `React` that returns two values: a state value and a method(or, function) to change that state value. We hold these two items in variables (*that's what you see on line 4: `const [isHidden, setIsHidden]`*). These two variables are defined by us, the developer. We could call them `const [isClicked, setClickedValue]` or anything else we want as long as it makes sense for what value they hold and change.
 
The syntax may look funny to you but it's just array destructuring. Using array destructuring we hold the values of what's returned from `useState()` as `[isHidden, setIsHidden]` to hold the value of state and create a method to change that value, respectively. When `setIsHidden` is called it will update `isHidden` with whatever argument is passed to `setIsHidden`. *See line 8 in the above example.*

## Are Class-based Components Being Replaced?

From the get go, you've been learning React through Class-based components so you can manage component state. Now we're asking you to switch to Functional components and use this new thing called Hooks instead of lifecycle methods and state. This may be frustrating but remember, React is the foremost front-end library in the world with wide adoption. Because of this, many applications are built with it. In the beginning of React, the only way to manage component state was through the use of Class-based components. Because of this you will likely see them in legacy code bases, Google searches, code examples on StackOverflow and equivalent forums. 

In the end it is important to know both because, the React development team has said they have no plans to remove Class-based components.

### Converting Class-based to Functional

Under the hood both Class-based components and functional components work exactly the same with DOM changes based on the state reference in memory. The examples below show the conversion of code from Class-based component to Functional Component using a hook to manage state.

=== "The Class-based Way"

    ```javascript
    // MyConditionalComponent.js
    import React, { Component } from 'react'

    class MyConditionalComponent extends Component {
        constructor(props) {
            super(props)
                this.state = {
                    isHidden: true
                } 
        }

        handleClick = () => {
            let status = this.state.isHidden == true ? false : true

            this.setState({
                isHidden: status
            })
        }

        render() {
            return (
                <div>
                    <h1 onClick={this.handleClick}>Functional Component Using State</h1>
                </div>
            )
        }
    }
    ```

=== "The Functional Component Way"

    ```javascript
    // MyConditionalComponent.js
    import React, { useState} from 'react';

    function App() {
        const [isHidden, setIsHidden] = useState(false);

        const handleClick = () => {
            let status = isHidden == true ? false : true
            setIsHidden(status);
        }
        return <h1 onClick={handleClick}>Functional Component Using State</h1>;
    }
    ```

=== "With Comments"

    ```javascript
    // MyConditionalComponent.js

    // Instead of importing the { Component }, let's import the { useState } hook
    import React, { Component } from 'react' 

    // No need to build a class, let's just keep it as a function: function App() {
    class MyConditionalComponent extends Component {
        // since it's not a class it doesn't need a constructor
        constructor(props) {
            // since it's not extending the React Component there's no need to call super()
            super(props)
            // we can store the value of state and the function to update it with destructuring instead of a state object: const [isHidden, setIsHidden] = useState(false);
            this.state = {
                isHidden: true
            } 
        }

        handleClick = () => {
            //   with a functional component we don't have state so need for all the extra member operators (.) : let status = isHidden == true ? false : true
            let status = this.state.isHidden == true ? false : true

            //  now, we don't need to pass an object to setState, instead, just use the function you defined earlier: setIsHidden(status);
            this.setState({
                isHidden: status
            })
        }

        render() {
            return (
                <div>
                    <h1 onClick={this.handleClick}>Functional Component Using State</h1>
                </div>
            )
        }
    }
    ```

Take some time to compare these two components. They accomplish the exact same thing but use different syntax to do it.

## See It - Components with Hooks

<!-- ! Video Contents: YT, TraversyMedia - Introducing React Hooks-->
<iframe width="655" height="368" src="https://www.youtube.com/embed/mxK8b99iJTg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

> The accompanying [Scotch.io/DigitalOcean Tutorial](https://www.digitalocean.com/community/tutorials/how-to-build-a-react-to-do-app-with-react-hooks)

<!-- @TODO Create Video here: 

VIDEO-1:
	- step by step converting a class component to functional using ComponentDidMount hook with beer app api
	- show a dummy component needing to use state and not having to change it to a class just add a hook (makes it useful to easily add state; in the past we had to change the entire component to class component)
	
VIDEO-2: 
    - Show how hooks work
	- passing props
	- changing state
	- useEffect dependencies 

-->

In the future, many videos & examples in pre-class lessons and some assignment work use Class-based components and have you'll have to know the Functional and Hook equivalent and be able to convert them your self.  

## Practice It

### Part 1

Below is a simple CodePen with a Class-based Component. Check out how the code works, what the app is doing, and then convert it to a Functional Component to make the app function the exact same way.

[Convert Class To Functional component with Hooks](https://codepen.io/instructorkc/pen/yLvpYjP?editors=1111)

### Part 2

<!-- https://studio.zollege.com/container/block-v1:ACA+JS411+09282020_JS411_C6+type@vertical+block@1d15a82226e549f99c5b67ea9a78ffd1 -->
<iframe src="https://codesandbox.io/embed/sharp-leakey-5z0fg?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="sharp-leakey-5z0fg"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

- [ ] Import `{ useState }` on the first line next to React
- [ ] Initialize the variables like in the example above. You will want a `count` and `setCount` with the default value being `0`
- [ ] Create an `<h3>` that displays the current count
- [ ] Create a button that uses `setCount` on its `onClick` method to change the `count`

## Additional Resources

- [ ] [Medium, Dan Abramov - Hooks](hhttps://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889ttps://medium.com/better-programming/4-ways-to-conditionally-render-in-react-3785fb5e5013)
- [ ] [YT, Fireship - 10 React Hooks Explained](https://www.youtube.com/watch?v=TNhaISOUy6Q)
- [ ] [YT, ReactConf - Dan Abramov: React 90% Cleaner](https://www.youtube.com/embed/dpw9EHDh2bM)
- [ ] [Blog, sarah_chima@dev.to - Array Destructuring](https://dev.to/sarah_chima/destructuring-assignment---arrays-16f)

## Know Your Docs

- [ ] [React Docs - Hooks](https://reactjs.org/docs/hooks-intro.html)
