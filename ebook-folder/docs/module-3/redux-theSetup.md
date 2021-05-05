# Redux: the Set Up

Ok. It's time to discuss how Redux works and how to set it up for any project. Yes, the setup is a bit tedious but the good thing is you only have to do it once per app. In the video below we breakdown the 4 major steps of setting up global state with Redux. You're asked to create a new repo but creating a new branch on your cars repo will be just fine:

## Redux: The First Four Steps

<!-- Video Content: Vimeo, Clayton@ACA - Redux:The First Four Steps -->
<iframe src="https://player.vimeo.com/video/492272459?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

- [ ] Create new repo or open your [Cars assignment](https://github.com/AustinCodingAcademy/411_wk4_day2_protected_routes) from a last class and create another branch called `implement-redux-global-state`

- [ ] Install Packages - The first thing we need to do is install two more npm packages into your project. They are `redux` and `react-redux`. To do so, run the following command: `npm i redux react-redux`.

### Setting Up State, Reducers, Store, And Provider

<!-- Video Content: Vimeo, Clayton@ACA - Setting Up State, Reducers, Store, And Provider -->
<iframe src="https://player.vimeo.com/video/492275873?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

- [ ] Setup the **State** Object - Next, we create a redux folder underneath/inside `src/` and add a `state.js` file to it. Inside that file is where we will put the default values for everything we want our entire application to be able to access in one big JavaScript object. We will also make sure it is exported. For example, a `state.js` file for our cars application will look like this:

=== "state.js File"

    ```javascript
      export default {
        user: null,
        cars: [ '1', '2', '3' ,'4' ]
      };
    ```

We'll keep it fairly simple for now with just two properties: `user` and `cars`.

- [ ] Build a **Reducer** - A reducer is a function that returns a representation of a specific piece of the state. Think of the reducer functions as a [reducing valve](https://www.cacciaplumbing.com/home-plumbing/what-is-a-pressure-reducing-valve-prv-and-why-do-i-have-one/). It reduces all of the state object down to smaller, very particular pieces of data so it can be easily consumed in any part of your application. Let's say you have an array of `dogs` and an array of `cats` but you only want the `dog` data in one component and the `cat` data in another but both data sets in a third component. We can do this easily by building two reducers: one for `cats` and one for `dogs`. These functions will *REDUCE* the state object `{dogs : [ ... ], cats: [ ... ]}` into two smaller bits of data: `dogs: [ ... ]` & `cats: [ ... ]`. See, the reducer functions reduces the larger state object into smaller much easier to use sets of data.

- [ ] To start, we need to create a `reducers.js` file underneath/inside the redux folder to tell Redux what state to send back to the application.

- [ ] This file will contain a function for each of the keys/value pairs of your state. If our state has two properties, `user` and `cars` we need two functions called `user` and `cars` that each take a **default parameter** named `state = []` or `state = null`. We use a [default parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) because reducers must **never** return `undefined`. For now, the functions will only return `state`, we'll change this tomorrow when we added **actions** to change `state`. Until then....

- [ ] ...let's bring-in/import another function from Redux called, `combineReducer`, that, as you might expect, *combines your reducers* into one usable reducer object.

  > NOTE: This by the way is creating an object-thing with keys to methods that are pointing to the value of your reducer functions. ...this is mostly unimportant to remember unless it helps you visualize what's going on here.

- [ ] At the bottom of the file we will `export` the combined reducers.

  > NOTE: Don't worry too much about this step now. It's necessary for the setup of Redux but we'll talk about it more in the next class because it's used for mutating the global state. In this lesson, we are just learning how to read the global state.

- [ ] Anyway, based on our `state.js` file our `reducers.js` file will look like this:

=== "reducers.js File"

    ```javascript
    import { combineReducers } from 'redux'

    const user = (state = null) => state

    const cars = (state = []) => state

    export default combineReducers({ user, cars })
    ```

- [ ] Create the **Store** - The next part is creating the **Redux store**. The "store" is our global application state. We will eventually connect it to the top of our application and that top component, `<App/>` or  `<Main />`, and everything underneath it will have access to the "store". A "store" is created using the `state.js` file we just created and some additional Redux components. We will create a `store.js` file underneath/inside in the `redux/` folder and it will look like this:

=== "store.js File"

    ```javascript
    import { createStore } from 'redux'
    import reducers from './reducers'
    import state from './state'

    export default createStore(reducers, state)
    ```

  > Simply put, we use the `createStore` method from `redux` to *create a store* with the given `reducers` and `state`.

- [ ] Wrap the **Provider** around the app - To tie in the `store`, `state`, and `reducers` together with our React app(function) we need to `import` and use the `{ Provider }` component from `'react-redux'` and provide our `store` in the `App.js` file. To do all of this, we will then "wrap" our application with the `Provider` component and pass the `store` as a prop called `store`.

=== "App.js File"

    ```javascript
      // import BrowserRouter and Router and Navigation from '../pathnameHere'
       import { Provider } from 'react-redux'
       import store from './store'

        function App() {
          return (
              <Provider store={store}>
                <BrowserRouter>
                    <Navigation />
                    <Router />
                </BrowserRouter>
              </Provider>
          );
        }
    ```

  > Note the `BrowserRouter`, `Navigation` and `Router` from last week.

**Setup Complete!!!** Ok . . . that sounds like a lot of set up (and it is) but we only have to do this **once**. Whenever we add new properties to your global state we simply need to put the new key/value in the correct places - *which we will practice in the coming homework*. For now, it's time to talk about our components being able to read from this global state we've so deftly created.
