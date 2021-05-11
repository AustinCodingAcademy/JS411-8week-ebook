# Redux `mapDispatchToProps`

Ok, it's time to hook up our actions to our components so that they work when we click a button, submit a form, etc. Right? We got this reducer with new `case`s and an action creator returning an actions object but now we need the components to have the ability to call or *dispatch* those actions!

To do that, we need to introduce a new tool called `mapDispatchToProps`. It's very much like the `mapStateToProps` tool we we've already learned to use. Let's look again at our `Home` Container in the `containers/` folder:

=== "Our Current `containers/Home.js` File"

    ```javascript
      import { connect } from 'react-redux'
      import Home from '../components/Home'

      const mapStateToProps = (state) => {
          return {
              cars: state.cars
          }
      }

      export default connect(mapStateToProps)(Home)
    ```

Let's import the `addCar` & `removeCar` function from `actions.js` file and add the `mapDispatchToProps` function tool so that we can bind/provide these actions to our component:

=== "containers/Home.js"

    ```javascript
      import { connect } from 'react-redux'
      import Home from '../components/Home'
      import { addCar, removeCar } from './actions'

      const mapStateToProps = (state) => {
          return {
              cars: state.cars
          }
      }

      const mapDispatchToProps = (dispatch) => {
          return {
              addCar: (car) => dispatch(addCar(car)),
              removeCar: (index) => dispatch(removeCar(index))
          }
      }
    ```

=== "with comments"

    ```javascript
      import { connect } from 'react-redux'
      import Home from '../components/Home'
      // import the two actions we want to provide to the component
      import { addCar, removeCar } from './actions'

      // we've already covered this but notice how this function returns an object with the key `cars` which is the name of the `prop` we use in the component: `props.cars`
      const mapStateToProps = (state) => {
          return {
              cars: state.cars
          }
      }

      // this function ALSO returns an Object with keys: `addCar` and `removeCar`...these will be accessed through `props` in the component as `props.addCar` and `props.??` Can you guess?
      const mapDispatchToProps = (dispatch) => {
        // return an object with keys that represent the `props` you'll want to use in the component.
          return {
              // we've passed in a parameter called `dispatch` which is just a name Redux's `connect` function is looking for. Then we use that `dispatch` function to create a value for each of the keys, see that?
              addCar: (car) => dispatch(addCar(car)),

              // we pass in the value to the anonymous function which then calls the `dispatch` function who then calls the actions creator we want it to use and gives it the value: `car` or `index`, in this case.
              removeCar: (index) => dispatch(removeCar(index))
          }
      }
    ```

The `mapDispatchToProps`(**MDTP** for short) function accepts a parameter called `dispatch`. **Remember to always include it there.** Then the **MDTP** function returns an object with keys that match the prop names you want to use in the "dumb" component. The value of each of these keys will be a function that returns/calls the `dispatch` function. Since you've already imported the actions you need(`{ addCar, removeCar } from './actions'`) you can call them inside the `dispatch` invocation and pass to it the value it will need to carry out it's action (`car` or `index`).

After you add the `mapDispatchToProps` to the `connect()` function, your "dumb" component will have access to the actions you've already built in `actions.js` through the prop names: `props.addCar` and `props.removeCar` [(see below)](#connect-mdtp). When these props are called, your reducers will be called and evaluate which action was created and return the new state back to the "dumb" component as props via `mapStateToProps`. It all comes full circle!

## Connect MDTP

Now, all that's left to do is `connect` this function to the component. It actually just comes right after the `mapStateToProps` argument which means the whole container file looks like this:

=== "containers/Home.js"

    ```javascript
      import { connect } from 'react-redux'
      import Home from '../components/Home'
      import { addCar, removeCar } from './actions'

      const mapStateToProps = (state) => {
          return {
              cars: state.cars
          }
      }

      const mapDispatchToProps = (dispatch) => {
          return {
              addCar: (car) => dispatch(addCar(car)),
              removeCar: (index) => dispatch(removeCar(index))
          }
      }

      // pass in the two functions as arguments to the `connect` function.
      export default connect(mapStateToProps, mapDispatchToProps)(Home)
    ```

Now the `Home` component has a prop called `cars` to receive the cars data from state and two props called `addCar` & `removeCar` which update the global state by adding the new `car` or the `index` to delete a car. They can be accessed anywhere in the component by referencing `props.cars`, `props.addCar`, or `props.removeCar`.

> The way it works: when we pass these functions to the `connect` function then immediately invoke the `Home` function we are creating a context around `Home` that gives it access to the two objects returned from each of the **MSTP** and **MDTP** functions.

## The Events in Order

1. At app start up, the `HomeContainer` is called **-->**
1. This will call the `connect` function which calls the **MSTP** & the **MDTP** functions who create objects with keys that point to the action functions in `actions.js` file **-->**
1. Then the "dumb" component function is called and created within this context so it has access to the state data and actions via `props` **-->**
1. From the "dumb" component, a form submit will call `props.addCar()` with a value: `"2008 Toyota Prius"` **-->**
1. Then the anonymous function, sitting at the `addCar` property on the object returned from the MDTP function, is called with the argument: `"2008 Toyota Prius"` **-->**
1. This calls the `dispatch()` function **-->**
1. Which then calls the `addCar()` action and passes the argument: `"2008 Toyota Prius"` **-->**
1. This fires the `addCar()` **Action Creator** function **-->**
1. Which returns an **Action** Object that will look like: `{type: ADD_CAR, value: "2008 Toyota Prius"}` to the reducer: `cars()` **-->**
1. The `cars()` reducer stop at the `case: ADD_CAR` and then creates a new array object using the current `state` plus the `value`: `"2008 Toyota Prius"` **-->**
1. Once state is updated the `connect` function will be called which calls the **MSTP** function who provides the new state to the "dumb" component **-->**
1. And the user sees the update on the screen. **-->**
1. Repeat. **-->**
1. Repeat. **-->**
1. Repeat. **-->**

> **MSTP** & **MDTP** are just abbreviations for the functions `mapStateToProps` and `mapDispatchToProps`

## Summary

- [ ] We create Redux **Action Creators** (again, these are just plain JS functions) that return **Actions**(just a plain ol' JS object) with the properties: `type` and `value`.
- [ ] Those Action objects are passed to the **Reducers** (just plain switch/case statements) that do and return different things based on `action.type` case.
- [ ] The container uses Redux's tools: `mapStateToProps`, `mapDispatchToProps`, and `connect` to give the component access to the global state properties and action creators to change that state via `props`. We tie all of that together in the container file so that the "dumb" component only manages visual representation presentation to the user.

> This follows right along with the [Single Responsibility Principle](https://medium.com/@severinperez/writing-flexible-code-with-the-single-responsibility-principle-b71c4f3f883f) of [SOLID](https://en.wikipedia.org/wiki/SOLID) programming.

