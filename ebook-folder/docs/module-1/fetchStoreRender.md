# Fetch Data & Store it in Local State

*You are in charge of your own destiny. You are the steward of your own vessel. And you have the power to choose, to grow, to learn, and to lead!*

## Overview

Now that we have a grip on this passing `props` stuff let's take a deeper look at that `state` stuff in **Class-based Components**. As you saw in the last lesson we were able to pass the values in a parent component's state down to its child component through **props**. But what is `state`? Where does it get its values? When is it created? In this lesson, we'll address all of those questions.

## Component State (Local Memory)

According to the [React Docs](https://reactjs.org/docs/state-and-lifecycle.html#adding-local-state-to-a-class), `state` is **locally-scoped memory**, which means that it is only available to the component that it is initialized in unless that data/memory is passed to another component via, ya know...`props`.

### The Rules of State

1. Only class-based components can have local `state`.
1. `state` is just a plain ole JavaScript object with key-value pairs.
1. If `state` changes the component **will** & **must** re-render.
1. `state` can only be updated with the `this.setState()` method which takes an object `{}` as its sole argument.

  > `setState()` compares the object you pass into the current state and changes only the values that need to change.

1. Again, `state` updates are **merged** which means `setState()` compares the object of `state` and the object passed into it before it makes changes and *only* changes what needs to be changed.

  > This is why `this.state` can only be changed with the `setState()` method.

1. The changes of `state` follow a pattern of data flow called a **top-down** or **unidirectional** data flow. *Data flows downward*. This means that `state` is always owned by some specific parent component, and any data or UI components derived from that `state` can only affect components *below* them in the tree.

### See It - State

#### Overview: Fetch, Store, and Render Data

<!-- ! Video Contents: Vimeo, Clayton@ACA - Overview: FetchStoreRenderData - 411.1.2.5 -->
<iframe src="https://player.vimeo.com/video/491877736" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

#### Fetch Data w/Axios + componentDidMount

<!-- ! Video Contents: Vimeo, Clayton@ACA - Fetch Data w/Axios + componentDidMount - 411.1.2.6 -->
<iframe src="https://player.vimeo.com/video/491880866" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

#### Map Over & Render Data
<!-- ! Video Contents: Vimeo, Clayton@ACA - Map Over & Render Data - 411.1.2.7 -->
<iframe src="https://player.vimeo.com/video/491885124" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

#### Render Functional Components + Styling

<!-- ! Video Contents: Vimeo, Clayton@ACA - Render Functional Components + Styling - 411.1.2.* -->
<iframe src="https://player.vimeo.com/video/491886398" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Practice It - State + Props

The homework is going to require you to code on your own a little more than usual. Why? Because the concepts of React are functional programming concepts and require doing to understand them. Also, you're becoming an actual developer, which means **you need to start learning to teach yourself**. Sooner or later there will be a new library or language you will need to know but don't. You then have to use your experience here to teach yourself that new library or language. Don't be afraid. You have the power of Google with you.

**BE SURE TO COMPLETE THIS BEFORE CLASS OR YOU WILL BE BEHIND!!**

Follow along with [the official React Tutorial](https://reactjs.org/tutorial/tutorial.html) to build an interactive Tic-Tac-Toe Game.

- [ ] Here's your [starter code](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)
  
    > You can do this either in CodePen or in a local environment folder. When you get it working in one, transfer it to the other.

- [ ] Start [here](https://reactjs.org/tutorial/tutorial.html#setup-option-2-local-development-environment).

## Additional Resources

- [ ] [YT, Ben Awad - State in React.js, pt.5](https://youtu.be/34fE23aib1o)
- [ ] [YT, Net Ninja - #17, Fetching Data useEffect](https://youtu.be/qdCHEUaFhBk?si=VqfoFe5u2eE9yASd)

## Know Your Docs

- [ ] [Legacy React Docs - State + Lifecycle Methods](https://reactjs.org/docs/state-and-lifecycle.html)

<hr>

- [ ] [React Dev Docs - Fetching Data w/Effects](https://react.dev/reference/react/useEffect#fetching-data-with-effects)
- [ ] [React Dev Docs - Synchronizing w/Effects](https://react.dev/learn/synchronizing-with-effects)