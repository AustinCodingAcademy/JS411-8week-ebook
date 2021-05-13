# Intro to React Hooks

*Happiness is not something you postpone for the future; it is something you design for the present. —Jim Rohn*

## Review and Recap

We've learned so much about front-end development with React over the course of the last six weeks. Today will be a free day to work on your final projects but we will cover React Hooks briefly in this pre-homework section. There will not be an assignment on it. But take the time to learn briefly about it so it's not a shock to you later, and then work on your Capstone Project before tomorrow's class.

## Overview

Just to reiterate . . . we are not taking a deep dive into this subject. We are bringing it up here because it is something you will see in the future and we just want to make sure you're prepared for it. Again, the next class is a free class for you to work on your final projects. That means you still come into class!

That being said . . . why use React Hooks? Well . . . because it allows us to use things like `state` in our functional components. When we say "state" here we mean local component state. Not global app state created by Redux.

## Read It - React Hooks

What are Hooks? They are simple pieces of React code that were added in 2018, to great fanfare among React developers. As we mentioned above, they allow you to use "state" in functional components (*not class components*). This promotes code cleanliness, only functional components, as well, code performance. The best way to learn about it is to just dive right in so we will look at an example.

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

If you remember, you can declare two variables at once using [array destructuring](https://dev.to/sarah_chima/destructuring-assignment---arrays-16f) and that's exactly what's happening here with `[count, setCount]`. Count will represent the value of state you want to use. Using regular state, this would look like this:

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

You'll notice that I set the `count` equal to `0`. The way that happened with React Hooks was on the second part of the first line, which reads `useState(0)`. The `useState` function is called with the initial value of the variable you want to set, `count`. So there's only one part left and that's the `setCount` variable. That variable represents a function and you call it when you want to change that particular piece of state! If we wanted to change the `count` to `1` we would write `setCount(1)` somewhere in the component. You can see an example of this in the button's `onClick` method. `<button onClick={() => setCount(count + 1)}>`.

Pretty simple stuff right? There are other hooks like `useEffect` that exist but we won't dive into those right now. We simply wanted to bring this to your attention because we know that you'll encounter it on your path to becoming front-end developers. One main place that you'll see Hooks used is in the Material UI documentation. Typically, when an update as popular as this happens, people start integrating it as quickly as possible.

Keep in mind that you are not required to use Hooks at all. Keep programming the way you have learned in React and Redux and everything will work just fine.

## See It - React Hooks

This first video is the introduction of Hooks at the React Dev conference in 2018. It's long and you do not need to watch the whole thing but some of it is pretty cool.

<!-- ! Video Contents: YT, ReactConf - Dan Abramov - React 90% Cleaner -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/dpw9EHDh2bM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

****

<!-- ! Video Contents: YT, TraversyMedia - Introducing React Hooks-->
<iframe width="655" height="368" src="https://www.youtube.com/embed/mxK8b99iJTg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

*****
*****

## Practice It

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

- [ ] [YT, Fireship - 10 React Hooks Explained](https://www.youtube.com/watch?v=TNhaISOUy6Q)
- [ ] [Blog, sarah_chima@dev.to - Array Destructuring](https://dev.to/sarah_chima/destructuring-assignment---arrays-16f)

## Know Your Docs

- [ ] [React Docs - Intro to Hooks](https://reactjs.org/docs/hooks-intro.html)
