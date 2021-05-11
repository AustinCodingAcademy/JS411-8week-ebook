# Update Reducers

Now that we have our actions it's time to update the functions in our `reducers.js` file. Actions communicate directly with the reducer responsible for a certain piece of state. That's the only way your Redux state gets updated. Each reducer is responsible for a specific piece of the state; it returns it in `mapStateToProps` and handles updates when called by `mapDispatchToProp` and given an Action to carry out. Again let's look at examples.

## Reducers as If/Else Statements

Before looking at these reducers assume the action creators we defined above are the actions being imported into this reducer file.

When we started, the reducer file looked like this:

=== "Our current `redux/reducers.js` File"

    ```javascript
      import { combineReducers } from 'redux'

      const user = (state = null) => state

      const cars = (state = []) => state

      export default combineReducers({ user, cars })
    ```

We're only focused on the `cars` part of these reducers right now so we'll update that reducer first.

As be rebuild this reducer, think of them as a large if/else statement, that is determining what it's supposed to do, based on the `type`: passed through it from the action creator. If `action.type === ADD_CAR` then the switch statement should stop at the `ADD_CAR` case and *add the `car` to state*. If it gets `REMOVE_CAR` it will stop there and remove the car from state. And the `default` case is to return the current `state` which is what we're already doing and passing to `mapStateToProps`. Let's add those first two cases into the `cars` reducer:

=== "Updated `redux/reducers.js` File"

    ```javascript
      import { combineReducers } from 'redux'

      const user = (state = null) => state

      const cars = (state = [], action) => {
          switch(action.type) {
              case 'ADD_CAR':
                  return [ ...state, action.value ]
              case 'REMOVE_CAR':
                  const newState = [ ...state ]
                  newState.splice(action.value, 1)
                  return newState
              default: 
                return state
          }
      }

      export default combineReducers({ user, cars })
    ```

=== "with comments"

    ```javascript
      // you know this, import the `combineReducers` tool from Redux
      import { combineReducers } from 'redux'

      // same as before, no changes made; just return the state so it can be `map`ped to `props`
      const user = (state = null) => state

      // still a reducers, which is just a JS function but with a second parameter now: `action`
      const cars = (state = [], action) => {
          // create `switch` statement based on the `type` property
          switch(action.type) {
              case 'ADD_CAR':
                  //  if the `type` is `ADD_CAR` then create a new array by spreading (...) `state` into it
                  // then add the `value` that came in with the action object
                  return [ ...state, action.value ]
              case 'REMOVE_CAR':
                  // if `type` is `REMOVE_CAR` then create a copy of the array by spreading `state` into it
                  const newState = [ ...state ]
                  // then `splice` our the car we want to remove but not directly on `state` instead using the copy we made
                  newState.splice(action.value, 1)
                  // finally, return the copy so it becomes the "new" `state`
                  return newState
              default: 
                // if there is no `type` to be evaluated just return `state` as is so it can be used my `mapStateToProps` as normal.
                return state
          }
      }

      // make these reducers available to the rest of the app with the `combineReducers` tool
      export default combineReducers({ user, cars })
    ```

Notice how we added the action argument as the second parameter to the cars reducer (which is just a Function). It represents the `action` that we're taking on this `state` and will have the two keys `type` and `value` in it.

In the switch statement, every case represents a possible type of `action`. *LOL, get it? "type of action"?* We then program the `cars` reducer to perform some operation on the state that corresponds with the `action.type` matches.

So the cars reducer is saying, if `action.type === "ADD_CAR"` add the new car (`action.value`) to the end of the state which represents the `cars` array in the `state.js` file (seen near the top of this page) and return the new state. If `action.type === "REMOVE_CAR"` resolves to true, then we want to `splice` the array based on the index we passed in with `action.value`.

  > A **very important note** about handling logic in the reducers: You always return a **copy** of the state. Not mutating the state itself. That's why we didn't write `state.push(action.value)` underneath the `"ADD_CAR"` case — because `push` doesn't return a new object, IT MUTATES THE ARRAY! Using the spread operator `[ ...   ]` returns a **COPY** of the array.*You should be familiar with these JavaScript operations from your 211 course. If not, spend some time brushing up on it.* We do this because of **[Pass By Reference](https://medium.com/@linuk/pass-by-reference-issue-i-encountered-in-javascript-c22f59f1196)** issues that could/will occur if multiple things are updating the state at one time. Don't worry about that too much, just understand that we **ALWAYS** pass a new object back from the reducer so Redux handles the actual updating of `state.js` and not our reducer functions.

## Summary

Each action `type` needs to have a corresponding `case` in the reducer otherwise the action will not be able to be carried out when *dispatched*.

Next up, we `connect` our actions to the "dumb" component's `props` with `mapDispatchToProps` (MDTP).