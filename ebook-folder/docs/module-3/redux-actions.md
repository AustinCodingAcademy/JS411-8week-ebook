# Redux Actions

*All you need is the plan, the road map, and the courage to press on to your destination. —Earl Nightingale*

## Review and Recap

Last week we learned how to use a plain object in a `state.js` file, functions in a `reducer.js` file and the Redux tools `combineReducers` and `<Provider />` to create a global state for our application that acts as a central data storage, or a **single source of truth**, for all of our app's components. Then we learned how to the data in in this global state to each component by wrapping them with another component/function with `mapStateToProps`. This process keeps all components in the app in sync with the same set of data so there is no confusion.

But now, we wonder how me might change the global state from a local component. How does a component get access to update a global state? The solution is a function called: `mapDispatchToProps`. Notice the similarity to `mapStateToProps`?

## Overview

We're continuing our learning of Redux because it's a great way to make sure all of our components share the same state. Remember, Redux doesn't actually do anything visually for the user of the application. This is all for the developer right now. Redux is strictly for data management. It will eventually allow you to do cool things like update charts instantaneously when data changes. Remember in your music controller app? If your volume component changed the global state of your app you might be able to create another component at the bottom of the dashboard that represented the amount of volume the user selected in a graph. If you're controlling data with Redux you can keep that data in one place but trigger the alert to your user that `"loud volume may cause hearing loss"` while also updating the chart to represent the level they chose. Again, Redux is a data management system for us developers to do cool things across the application using one source of truth. So any direct benefit to the user comes with the fact that Redux allows us to develop more complex applications.

Also, keep this in mind . . . Redux is not completely replacing **local state**. If you want a component to be able to toggle between two states, for example on/off, you can still use:

```javascript
  state = {
    on: true
  }

  // ...more code...this.setState({ on: !this.state.on })
```

In the above code, this component, and only this component, will have access to `this.state.on`. Redux is for when you want to share a central state data across multiple components. It's important that we are clear on the difference there.

### See It - ActionCreators & `mapDispatchToProps`

<!-- !Video Content: Vimeo, Clayton@ACA - 411-41-ActionCreators&MapDispatchToProps - 411.3.3.1 -->
<iframe src="https://player.vimeo.com/video/492290141?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Actions

The first thing we need to build so our components can update/mutate state is create something called **Redux Actions**. Actions are simply JavaScript Objects. They typically have two properties (although you may see others), a `type` and a `value`. They look like this:

=== "A Redux Action"

    ```javascript
      const addCar = {
          type: 'ADD_CAR',
          value: 'Tesla Model Y'
      }
    ```

Spelling the value of `type` in capital letters, like `'ADD_CAR'` is a Redux convention. It lets other developers on your application know that you are using Redux. The value of `value` is whatever you want to update your state with.

  > NOTE: Another common practice is to use the key name `payload` instead of `value` for the simple verbalization trickery. "What is the value of `payload`?" is easier to say than "What is the value of `value`?" Nevertheless, we'll use `value` for this lesson...

Furthermore, it has become less common to use plain actions (seen above, a simple JS Object). Instead, we build **Action Creators**. Action creators are simply functions that return an action. That means, its just a JS Function that returns and JS Object. So instead of the syntax above, we change it to:

=== "Action Creator function"

    ```javascript
      const addCar = (newCar) => {
          return {
              type: 'ADD_CAR',
              value: newCar
          }
      }
    ```

As you can see, it's just a function that returns an object. But why? Well. . . take a look at the action creator above and notice that it has an argument, `newCar`. With action creators we can pass options to our action creating functions and have them return different things each time they're called. This is more powerful than plain action objects because it can dynamically respond to user's input. *We will be using **Action Creators** going forward.*

Finally, the last thing you need to know about actions is that they correspond to a certain piece of the global state. Only you, the developer, get to decide what corresponds to what. So for example, we have an action called `ADD_CAR` above. It makes sense that we would use this action to update the `cars` property in state. Remember this example from our last pre-work:

=== "Global State - `redux/state.js`"

    ```javascript
      export default {
          user: null,
          cars: [ '1', '2', '3' ,'4' ]
      }
    ```

We want to make actions that make sense for our data model. Since `cars` is an array, two common operations would be add to and remove a car from the array. So `cars` might have the following actions:

* `ADD_CAR` - push a new car value on to the array.
* `REMOVE_CAR` - delete a particular car from the array.

Likewise for the `user` property. It's `null` right now but it could probably represent an Object or maybe just a plain String. Either way, actions that make sense for this property would be:

* `SET_USER` - set which user is signed in right now.
* `UNSET_USER` - remove the user at sign-out.

  > Again, the CAPITALIZED_UNDERSCORE naming convention is a Redux convention.

You get to name these as you like, so make sure they make sense to you and other developers. Remember, code is NOT what a computer reads. **Code is what humans read.**

Final note about action creators: they all go in a single file called `redux/actions.js` (inside of the "redux" folder) like below.

=== "`redux/actions.js` File"

    ```javascript
      export const addCar = (newCar) => {
          return {
              type: 'ADD_CAR',
              value: newCar
          }
      }

      export const removeCar = (index) => {
          return {
              type: 'REMOVE_CAR',
              value: index
          }
      }

      export const setUser = (newUser) => {
          return {
              type: 'SET_USER',
              value: newUser
          }
      }

      export const unsetUser = (index) => {
          return {
              type: 'UNSET_USER',
              value: index
          }
      }
    ```

The next step is to update our Reducer functions to accept and respond to these incoming Action Objects.