# Containers, Connect() & mapStateToProps()

<!-- !Video Content: Vimeo, Clayton@ACA - 411-39-ConnectStateToComponentViaProps -->
<iframe src="https://player.vimeo.com/video/492284143?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

- [ ] A `Container` is simply a higher-order component that's connected to our Redux Store and returns a React Component but provides data from the Store to it first. For organizational sake, we'll create a new folder called `containers/` to hold these container component.

In the cars example, we've been working on, we used a component called `Home` to list all of our cars. Let's create a new file with the same name (`Home.js`) in our containers folder and connect it to Redux.

- [ ] Redux works by taking the state variables we want and mapping them to props in our component. So if we want to connect `Home` to the value of `cars` from our `state.js` file, the value will be mapped to a `prop` that we specify (likely as `cars`) and then we will access it in the component by calling `props.cars`. Redux provides a function for doing that called `mapStateToProps` and we connect it to our component using the `connect` function. Let's see an example:

=== "containers/Home.js File"

    ```javascript
    import { connect } from 'react-redux'
    // import the visual React component "Home"
    import Home from '../components/Home'

    const mapStateToProps = (state) => {
        return {
            cars: state.cars
        }
    }

    // wrap the visual React Component "Home" with the Redux Container Component Home
    export default connect(mapStateToProps)(Home)
    ```

- [ ] We first import the `connect` function from Redux and our **"dumb"/visual component**. Then we build a `mapStateToProps` function that builds an object with a key, `cars` to be set to `state.cars`. Remember, `state.cars` is what exists in our `state.js` file. From there, we can export the Higher-Order Component(**HOC**) which will make `state.cars` (now `cars` available to our "dumb" component, `<Home />` as `props.cars` using the [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) `(Home)`.

- [ ] Now we just need to reference it in a couple of places to make full use of it. In our `Router.js` file where we're used to importing: `import Home from '../components/Home'` we now import: `import Home from '../containers/Home'`. This change is how we can start understanding why the term **"dumb component"** was coined. See, a regular React component just returns what it's told to return via its `props`. But now we're introducing this HOC, which calls the regular React component and provides the `props` to be rendered. So, in a sort of colloquial jargon, we say a regular React component is a **Dumb component** and a redux component is a **Smart Component/Container**. Rude, right?

- [ ] Back in our dumb `Home` component where we had imported `cars.json` and did `cars.map`... it's now `props.cars.map` and we no longer need the `cars.json` file because that data is now in `state.js`. Additionally, this can now be done on any other component we want and all of them would have access to `cars`!

  > You might be thinking . . . we could have just imported `cars.json` everywhere we wanted to use cars and you're right, but it wouldn't be **dynamic**. It wouldn't act like **state** is supposed to act. In this manner, (with Redux), eventually, when we update "cars" from one component, all other components that are using the data will be notified automatically. That is the real power of Redux and we will explore that in the next lesson.

## Review Connect() + Practice It

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-40-ConnectReview&FolderRe-Org - 411.3.1.* -->
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/492287220?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="411-40-ConnectReview&amp;amp;FolderRe-Org"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

### Push Yourself Further

<!-- ! Contents: CodeSandBox, Redux Practice -->
<iframe src="https://codesandbox.io/embed/nice-feather-9787d?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="nice-feather-9787d"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

- [ ] Open the sandbox above. Notice the two components (`MyComponent`, `MySecondComponent`)
- [ ] Notice the way the data is currently passed. That is, if we want two components to have the same data we currently have to define that data on the parent component (`App`) and then pass it to the two components with props: `items={items}`

  > NOTE: most of the Redux set up has been done for you in this example

- [ ] In `index.js` import the `Provider` and the `store`. (Uncomment line 5 & 6)
- [ ] Wrap the `<div className="App">` with the `<Provider>` and pass the store as a prop named `store` to the `Provider`
- [ ] Go to the `containers/` folder. In each file, write a `mapStateToProps` function (it will be the same for both). Remember to `connect` it and `export` it
- [ ] Then, go back to `index.js` and replace the imports at the top so that they reference the containers instead of the components directly. Ex. `../containers/MyComponent`.
- [ ] Delete the `const items` and the passing of props to `MyComponent` and `MySecondComponent`
- [ ] Is the app still working? It should work exactly the same as before. Try adding a third item in `redux/state.js`. Did both components receive the update?
- [ ] If not, reload and rework through these steps again

## Additional Resources

- [ ] [YT, PentaCode - How To Add Redux To Create React App (1/3)](https://www.youtube.com/watch?v=eN6CfnTDsQc)

## Know Your Docs

- [ ] [Redux Docs - Getting Started](https://redux.js.org/introduction/getting-started)
