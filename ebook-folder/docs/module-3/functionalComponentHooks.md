# Functional Components with Hooks

*Trust the process.*

## Replace Class Components With Functional Components using Hooks

#### We just learned about class Components why did we learn them and now have to replace them? 
Class components have been part of React since the beginning and were the only way to manage state. Hooks were introduced with version 16.8 and they brought the power of state management to functional components. Developers now favor functional components with hooks when writing new code.    

Here is a scenario that demonstrates a use case for why developers favor functional components with hooks. Lets say Last week you made this simple display component.

=== "Functional Component"

    ```javascript
    import React from 'react'

    function App() {
       return <h1>Simple Functional Component</h1>
    }
    ```

 We are tasked to add state to toggle visible and hidden status. Before hooks we would have to go through the process and convert it to a class component now we can just add a useState hook.   
       
=== "State managemnt using hook useState"

```javascript
  import React, { useState} from 'react';
   function App() {
    const [isHidden, setIsHidden] = useState(false); //useState is a Hook

    const handleClick = () => {
        let status = isHidden === true ? false : true
        setIsHidden(status);
    }
    return <div>
             <p>The Status of hidden is {isHidden}</p>
             <h1 onClick={handleClick}>Functional Component Using State</h1>
          </div>;
  }
```
 `useState()` is a hook imported from `React` that returns two values that we can using array destructuring to hold and change state with `[isHidden, setIsHidden]` respectively. The first value is the state initiated by the useState argument and the second is like setState except we can give it a name. This is an example of one of the many advantages of functional components with hooks and including but not limited to code cleanliness, versitility and reusabilty.


#### Why learn class components if they are being replaced going forward?
When you google questions about React many of the answers from documentation, code examples on stack overflow and equivalent sites will use class based components because the answer is still valid so you need to know how to use both and convert it to a hook. In addition, Many legacy projects from open source projects to commercial applications still utilize class components. In the end it is important to know both because, the React development team has said they have no plans to remove class components.

## Convert class Component to functional component with hooks, 
Under the hood both class components and functional components work exactly the same with DOM changes based on the state reference in memory. The example below shows the conversoin of code from Class component to Functional Component using a hook to manage state.

=== "Class Component"

    ```javascript
       // FUNCTIONAL CODE IN COMMENTS!
    {import React, { Component } from 'react' //  import React, { useState} from 'react';

    ///     function App() {
    class MyConditionalComponent extends Component {
     
    constructor(props) {
        super(props)
    // const [isHidden, setIsHidden] = useState(false);
        this.state = {
        isHidden: true
        } 
    }


    handleClick = () => {
    //   let status = isHidden == true ? false : true
    let status = this.state.isHidden == true ? false : true

    //  setIsHidden(status);
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
    }
        
    ```

=== "Converted to Functional Component"

    ```javascript
    

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

#### Bellow is an important video showing the proccess of converting a class to functional component and using hooks to manage state.

<iframe src="https://player.vimeo.com/video/491877736" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

<!-- ! VIDEO:
	Show converting a class component step by step to a hook (use ComponentDidMount and beer 	app api)
	show a dummy component needing to use state and not having to change it to  a class just add    	makes it usefull to easily add state (in the past we had to change the entire component to class          	component)
	Show how hooks work
	passing props
	changing state
	 useEffect dependencies -->

In future videos examples and assignments you will see class components and have to know the hook equivalent and be able to  convert them your self. Many examples in pre-class and some assignment work uses class components and you will have to understand the hook equivalent.

## Practice It

This CodePen is to learn how to convert a class based component to a hook and then use knowledge from the video to implement useEffect!

[Convert Class To Function component with Hooks](https://codepen.io/instructorkc/pen/yLvpYjP?editors=1111)

## Additional Resources
- [ ] [Blog, Medium - Hooks](hhttps://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889ttps://medium.com/better-programming/4-ways-to-conditionally-render-in-react-3785fb5e5013)

## Know Your Docs

- [ ] [React Docs - Hooks](https://reactjs.org/docs/hooks-intro.html)

