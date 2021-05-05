# App State with Redux

*Try to be a rainbow in someone’s cloud. —Maya Angelou*

## Review and Recap

We've integrated routing into our application and even learned how we can protect some of our routes from being accessed if a user isn't logged in. What if now we need to get the logged-in user's information to be used in any component? That would be very expensive to make a network request(`ajax`, `fetch`, or `axios`) for every component...every time it loaded. Let's introduce a global state management system called Redux to keep up with an **App State** so we can store that data.

Remember, with a class-based component we have **local state**: `this.state = { /* some key/value pairs */ }`. But for a more managing an app's **global state**, that is, a **single source of truth** our entire app can access, we'll need to create it in another place. Redux happens to be the gold standard for something like this. Here goes!!

## Redux: the High Overview

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-35-ReduxHighOverview - 411.3.1.1 -->

<iframe src="https://player.vimeo.com/video/492266641?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## What is Redux?

This is a definition from the [Redux website](https://redux.js.org/introduction/getting-started).

  > Redux is a predictable state container for JavaScript apps.

  > It helps you write applications that behave consistently, run in different environments (client, server, and native), and are easy to test. On top of that, it provides a great developer experience, such as live code editing combined with a time traveling debugger.

  > You can use Redux together with React, or with any other view library. It is tiny (2kB, including dependencies), but has a large ecosystem of addons available.

Let's talk about it in more layman's terms and provide some examples.

We're used to seeing something like this to build a simple React component that is showing a status (on/off) based on the state:

```javascript
  import React, { Component } from 'react'

  class MyComponent extends Component {
      state = {
          on: true
      }

      render() {
          return (
              <div>
                  <p>The status is: ${this.state.on ? 'On' : 'Off'}</p>
              </div>
          )
      }
  }

  export default MyComponent
```

What if we make a new component called `MySecondComponent`:

```javascript
  import React, { Component } from 'react'

  class MySecondComponent extends Component {
      render() {
          return (
              <div>
                  <p>This is my second component</p>
              </div>
          )
      }
  }

  export default MySecondComponent
```

Does `MySecondComponent` have access to the state (`on`) of the original `MyComponent`? Of course not. Normal React state only works within the component in which it's defined. So `MySecondComponent` doesn't have any idea what state `MyComponent` is in unless we pass the state down as `props`, but as you've probably already seen, passing `props` down, to only pass more `props` down becomes tedious, ugly, and unmanageable. Like filling a cup to pour into another cup and then to only pour into yet another cup. But we can change that process with Redux.

But first. . . why would we want to do that? Well . . . the previous example might be too specific. `MySecondComponent` and `MyComponent` might not need to know about each other or each other's state, but what about if instead of `on`, `MyComponent` had the user data for the logged-in user? Then `MySecondComponent` might want to know about it because it may want to access it at some point in the future. We will eventually handle this by moving the `state` out of `MyComponent` and into a **global** Redux **state** that both components will have access to. Whenever one component changes the `state`, i.e. `user`, the other one will know about it. That's the power of Redux!

Before we dive into some examples, let's briefly talk about what Redux is doing and what it **isn't doing**.

### What is Redux doing?

Redux is helping the DEVELOPER structure the app in a way that makes it simpler for cross-component communication. It helps us limit the passing of props to many different components that need the same information. Simply put, Redux helps define a **single source of truth** that can be shared with all components simultaneously without passing props.

### What is Redux NOT doing?

1. Redux is **not** providing any new styling or logic that the end-user is aware of. The site will look exactly the same.
2. The user will see **no** difference, but the developer will be able to add advanced functionality more rapidly.

### Redux: Visualize the Global State(App State)

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-36-ReduxVisualizeGlobalState - 411.3.1.2 -->
<iframe src="https://player.vimeo.com/video/492269518?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

