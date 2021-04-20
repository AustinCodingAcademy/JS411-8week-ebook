# Conditional Rendering

*The harder you work for something, the greater you’ll feel when you achieve it.*

## Overview

Whoa, you've done a lot! Already you've learned the core mindset and techniques of React which includes a new language, JSX!! Congratulation!

In the past few lessons you've learned how to fetch data, store it in state and rendering it for the human-user's eyes using someone else's code base, React. During that time you've learned how to merge our understanding of programming in JavaScript with the layout and styling of HTML and CSS. We've been working hard! But now it's time to dig a little deeper and figure out how to use some of the statements we learned last week to render certain elements based on conditions that we get in our applications.

## Conditional Rendering Using Local State

Below is a snippet of code that should be very easy for you to read.

=== "Simple If/Else Statement"

    ```javascript
    if (isVerified) {
      return "is verified"
    } else {
      return "not verified"
      }
    ```

This is simple and straightforward JavaScript. We'll now just apply the same logic with React. After all, when we're developing in React we're writing JavaScript!

=== "If/Else Statement in React"

    ```javascript
    import React, { Component } from 'react'

    const MyConditionalComponent = (props) => {
      if (props.isVerified) {
        return <IsVerifiedComponent userId={props.id} />
      } else {
        return <NotVerifiedComponent userId={props.id} />
      }
    }
    ```

Above we see that if the user is verified, `(prop.isVerified = true)` then we can render a component that might welcome the user like the `<IsVerifiedComponent />`, else we can render a component that tells them that their login failed and ask them to try again in the `<NotVerifiedComponent />`.

All of that was based on the values that are in the `props` object. We can do the same thing with state! Follow along with the comments throughout the code snippet to understand this for yourself.

=== "Button Changes State"

    ```javascript
    // turn your functional component into a class-based component so you can create local state

    import React, { Component } from 'react'

    class MyConditionalComponent extends Component {
      constructor(props) {
        super(props)

        /* inside the constructor, initiate the state as an object and give it the keys you want to use, in this case we'll use a property called isHidden so we know what it's for. */

        this.state = {
          isHidden: true
        }
      }

    /* Remember from 211 that classes are functions that return an object with a context or instance of which will require/allow us to use the `this` keyword. */

      /* because the component is a class we can also create and use our own methods: */

      handleClick = () => {
        /* What you see below is a ternary operator. It reads like this: "if this.state.isHidden is true - set status to be false , else set it to true". */

      let status = this.state.isHidden == true ? false : true

        /* Because we have the variable status set to be the opposite of whatever this.state.isHidden equals... */

        /* ...we can use its value to set this.state.isHidden when our button is clicked.*/

        /* Notice we use the .setState({}) method to change values in our state object. */

      this.setState({
        isHidden: status
        })
      }

      render() {
        /* then we check if the value in state is true or false and render accordingly */
        if (this.state.isHidden) {
          return (
            /* if the user clicks this component it will trigger the handleClick method which changes the state and then forces the parent component to re-render, which will render the `<UserDetailsCard />` component as well and vice versa! */
            <UserNameCard revealClick={this.handleClick} userId={props.user.id}/>
          )  
        } else {
          return (
            <div>
              <UserNameCard userId={props.user.id}/>
              <UserDetailsCard hideClick={this.handleClick} userId={props.user.id} />
            </div>
          )
        }
      }
    }
    ```

=== "without comments"

    ```javascript
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
        if (this.state.isHidden) {
          return (
            <UserNameCard revealClick={this.handleClick} userId={props.user.id}/>
          )  
        } else {
          return (
            <div>
              <UserNameCard userId={props.user.id}/>
              <UserDetailsCard hideClick={this.handleClick} userId={props.user.id} />
            </div>
          )
        }
      }
    }
    ```

In the example above we will have to assume `<UserNameCard /> `and `<UserDetailsCard />` have a button in them that looks like this: `<button onClick={this.props.revealClick}>Show Details</button>` and `<button onClick={this.props.hideClick}>Hide Details</button>`. Each of these buttons have a built-in property called `onClick`. We then assign the `onClick` method to `this.props.revealClick` which then points back to the original method we built: `handleClick`.

In short, when the button is clicked it sends data back up to its parent components to change the value of `this.state.isHidden`. In turn, when the state changes, React will re-render and we'll get a new view because `MyConditionalClass` has a conditional rendering if/else statement in it.

You will be using this for your next few projects so read back over it and make sure you got it!

  > NOTE: in the normal DOM methods you have seen `onclick` but in React you will use `onClick`

For further reading check out the Medium blog on Conditional Rendering in the [Additional Resources](#additional-resources).

In the upcoming video you'll see a different way to manage conditional rendering using the newer method, `useState()` hook. Both ways work and this "older" way is taught first because it used to be the *only* way to manage this task before [React introduced Hooks](https://reactjs.org/docs/hooks-intro.html).

### See It - Conditional Rendering

You are welcome to use either method you feel most comfortable with but we would be remiss if you didn't learn how to use the new Hook, `useState()`, to do the same thing and not create a Class-based Component only to manage a state object...!

<!-- ! Video Contents: Vimeo, Clayton@ACA - ConditionalRenderWith-useStateHook - 411.1.3.1 -->
<iframe src="https://player.vimeo.com/video/492113241" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Additional Resources

- [ ] [YT, Codevolution - Conditional Rendering](https://youtu.be/7o5FPaVA9m0)
- [ ] [Blog, Medium - Conditional Rendering](https://medium.com/better-programming/4-ways-to-conditionally-render-in-react-3785fb5e5013)

## Know Your Docs

- [ ] [React Docs - Hooks](https://reactjs.org/docs/hooks-intro.html)
- [ ] [React Docs - Lists & Keys](https://reactjs.org/docs/lists-and-keys.html)
