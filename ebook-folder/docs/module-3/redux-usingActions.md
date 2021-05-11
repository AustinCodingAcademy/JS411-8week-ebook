# Using Action Creators + Challenge

<!-- ! Video Contents: Vimeo, Clayton@ACA - TITLE - 411.3.3.2 -->
<iframe src="https://player.vimeo.com/video/492294307?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Practice It
<!-- ! Contents: CodeSandBox, Redux Action Practice -->
<iframe src="https://codesandbox.io/embed/autumn-sun-o9syi?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="autumn-sun-o9syi"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

- [ ] Open the sandbox above. Take a look around and see the file setup that we currently have. Notice that Redux files have been completely set up for you. Your job is to add actions, update the reducer and add the `mapDispatchToProps` function to the `connect`. *Just like what you've just finished learning...*
- [ ] Create an `actions.js` file underneath the "redux" folder.
- [ ] Inside this file, export a function called `addUser` with a `type` property: `"ADD_USER"` and a `value` property that points to the parameter: `user`. It should look like this:

```javascript
  export const addUser = user => {
    return {
        type: "ADD_USER",
        value: user
    }
  }
```

- [ ] Go to the `reducers.js` file. Update the reducer with a switch/case statement. It should add a user to the array if the `type` is `"ADD_USER"`. On the default option, simply `return state`.
- [ ] Go to the `UserList` CONTAINER and import your action `addUser` at the top of the file. Now create a `mapDispatchToProps` function that returns and object with a property called `addUser` which points to the value of the `addUser` action creator you just imported. Don't forget to wrap it in `dispatch()`.
- [ ] Once that is set up, go to the `UserList` COMPONENT and add an `onClick` method to the button. It should reference `props.addUser` and it should send along the `newUser` variable like this: (`) => props.addUser(newUser)`
- [ ] Click the button. See how the new user gets added to the list? Additionally, see how every time a new user is added, the `UserCount` component automatically gets updated and knows how many users exist in the `UserList` component? We are starting to see some of the power of Redux.

*****

## Know Your Docs

- [ ] [Redux Docs - Getting Started](https://redux.js.org/)

## Additional Resources

- [ ] [YT, thenewboston - Actions and Action Creators](https://www.youtube.com/watch?v=_x3gitcwtAc)
- [ ] [Article, linuk@Medium - Pass By Reference](https://medium.com/@linuk/pass-by-reference-issue-i-encountered-in-javascript-c22f59f1196)
- [ ] [Article, severinperez@Medium - Single Responsibility Principle](https://medium.com/@severinperez/writing-flexible-code-with-the-single-responsibility-principle-b71c4f3f883f)
- [ ] [Wikipedia, SOLID Programming](https://en.wikipedia.org/wiki/SOLID)
- [ ] [Redux Docs - `bindActionCreators()`](https://redux.js.org/api/bindactioncreators)

### Optional, bindActionCreators

If you're feeling confident and comfortable with this process, you may use the `bindActionCreators` method from redux to simplify your code a little bit. *But this is very optional!!*

=== "`containers/Home.js` using `bindActionCreators`"

    ```javascript
    import { connect } from 'react-redux'
    import Home from '../components/Home'
    // import bindActionCreators tool to be able to use it
    import { bindActionCreators } from 'redux'
    import { addCar, removeCar } from './actions'

    //...code removed for simplicity...
    //...MSTP function here...

    const mapDispatchToProps = (dispatch) => {
        return bindActionCreators({ addCar, removeCar }, dispatch)
    }

    export default connect(mapStateToProps, mapDispatchToProps)(Home)
    ```

=== "`containers/Home.js` as before"

    ```javascript
    import { connect } from 'react-redux'
    import Home from '../components/Home'
    // import bindActionCreators tool to be able to use it
    import { bindActionCreators } from 'redux'
    import { addCar, removeCar } from './actions'

    //...code removed for simplicity...
    //...MSTP function here...

    const mapDispatchToProps = (dispatch) => {
      return {
          addCar: (car) => dispatch(addCar(car)),
          removeCar: (index) => dispatch(removeCar(index))
      }
    }

    export default connect(mapStateToProps, mapDispatchToProps)(Home)
    ```
