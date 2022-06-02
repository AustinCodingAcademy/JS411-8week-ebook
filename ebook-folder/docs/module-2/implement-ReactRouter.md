# Implementing React-Router

## Overview

Now that you've gotten a hold of this new tool and have an understanding of why and when to use it, let's take some time to see how it's implemented so you can really get the flow of these "wrapper"/higher-order components.

## Implement BrowserRouter

=== "Implement BrowserRouter Video"

    <!-- ! Video Contents: Vimeo, Clayton@ACA - 411-29-ImplementingBrowserRouter - 411.2.3.1 -->
    <iframe src="https://player.vimeo.com/video/492232669?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
     
    > NOTE: This video was recorded before React v8 and the rendering method for React is now `ReactDOM.createRoot()` which is imported from "react-dom/client". Your example might look like this:
      ```javascript
      import ReactDOM from "react-dom/client";
      import "./index.css";
      import App from "./App";

      const root = ReactDOM.createRoot(document.getElementById("root"));
      root.render(<App />);
      ```

=== "Video Outline"

    - [ ] Go to `index.js`
    - [ ] `import { BrowserRouter } from 'react-router-dom'`
    - [ ] create new component

      ```javascript
        const Main = () => {
          return (
            <BrowserRouter>
              <Router />
            </BrowserRouter>
          )
        }
      ```

    - [ ] and `import Router from './Router'`
    - [ ] replace `<App />` with wrapper function `<Main />`

## Building the Router Component

=== "Building the Router Component Video"

    <!-- ! Video Contents: Vimeo, Clayton@ACA - 411-30-BuildingTheRouterComponents - 411.2.3.2 -->
    <iframe src="https://player.vimeo.com/video/492236276?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

    > NOTE: This video was recorded before reactRouter v6. We don't use `<Switch>` anymore. It is now `<Routes>`. Your example should look more like this:  
    ```javascript
      import React from 'react';
      import { Routes, Route } from 'react-router';
      
      import App from './App';
      import Home from './Home';

      const Router = () => {
          return (
              { /* Then we use Routes and Route. Routes acts like a regular JS Switch Statement */ }
              <Routes>
                  { /* depending on the path in the URL, one of these Routes will be returned and their component rendered */ }
                  <Route path="/home" element={<Home/>} />
                  <Route path="/app" element={<App/>} />
              </Routes>
          );
      }

      export default Router;
    ```

=== "Video Outline"

    - [ ] Create `Router.js file`
    - [ ] import `React`
    - [ ] import `Routes` & `Route`
    - [ ] Import the two components you want to test with!!!
    - [ ] `import React from 'react'`
    - [ ] `import { Routes, Route } from 'react-router-dom'`
    - [ ] `import Home from './Home'`
    - [ ] `import App from './App'`
    - [ ] Create Router function/component:

      ```javascript
        const Router = () => {
          return (
              <Routes>
                  <Route path="/home" component={Home} />
                  <Route path="/app" component={App} />
              </Routes>
          )
        }
      ```

    - [ ] Dont forget to: `export default Router`
    - [ ] Go back to `index.js` and uncomment the import!!
    - [ ] Test your App to see if it works!

## Implementing Link

=== "Implementing Link Video"

    <!-- ! Video Contents: Vimeo, Clayton@ACA - 411-31-ImplementingLink - 411.1.1.* -->
    <iframe src="https://player.vimeo.com/video/492243077?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

=== "Video Outline"

    - [ ] 1. Go to the simple components: `<HelloWorldOne />` & `<HelloWorldTwo />`

    - [ ] 2. `import { Link } from 'react-router-dom'`

    - [ ] 3. Add your wherever you want!!!

    - [ ] 4. `<Link to="/yourpath">`

    - [ ] 5. Remove underline... `style={{ textDecoration: "none" }}`

    - [ ] 6. Use a Material-UI Button... `import Button from "@mui/material/Button";`



      ```javascript
        <Link to="/home">

          <Button style={{ margin: "5% auto"}} variant="outlined" color="primary">

            Go BackHome

          </Button>

        </Link>
      ```

    - [ ] 7. Create two more components called: `<SignIn />` & `<SignUp />` and give them all Links to go to

      * `<HelloWorldOne />` & `<HelloWorldTwo />` & `<SignIn />` & `<SignUp />`

    - [ ] 8. Bonus 1: Use a Material-UI Button Group to do it!!!

    - [ ] 9. Bonus 2: Create a new component for the Button Group and import it into the other four components:

      * `<HelloWorldOne />` & `<HelloWorldTwo />` & `<SignIn />` & `<SignUp />` or whichever components you've decided to use.

## Another Method to Implement Link with MUI Button
MUI will also accept another property named `component` which can take the value of any component we want to render in it's place. By doing this, we will not need to overwrite `Link`'s default styling since MUI will overwrite it using this method. You can now also add the `to` property, which we can specify the route we want to navigate to, to our `Button`, and now our `Link` will have access to that `to` property as well.
Here is an example on how to implement Link and MUI's Button:
```javascript
  // Of course, don't forget your necessary imports...

  <Button component={Link} to="/login" variant="outlined" color="primary">
    Login
  </Button>
```
You can refer to MUI's [Button API](https://mui.com/material-ui/api/button/) to see a list of different properties the Button component may take.
## Practice It

<!-- ! Video Contents: CodeSandBox - React Router Basics -->
<iframe src="https://codesandbox.io/embed/react-router-dosker?fontsize=14&hidenavigation=1&theme=dark"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="React Router - Basic"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>

### Practice Section Instructions

- [ ] Open the code editor and navigate to `App.js` on the left-hand side
- [ ] The dependecies have already been imported for you. Notice the imports from `"react-router-dom"` and `"@mui/material"`
- [ ] We also have a custom Router component being imported. Let's look at the Router file next.
- [ ] The dependecies have also been imported here for you, `import {Routes, Route} from "react-router-dom"`
- [ ] We also have some simple custom Components being imported here as well, `"Dashboard"` and `"Login"`
- [ ] Follow the TODO's marked in the comments of both the App.js and Router.js files.
- [ ] Practice making other `Route`'s and apply the same logic. Pretty Simple!

## Additional Resources

- [ ] [YT, PedroTech - React Router v6](https://www.youtube.com/watch?v=UjHT_NKR_gU)
- [ ] [Reference, StackOverflow - Link](https://stackoverflow.com/questions/51642532/how-to-make-a-material-ui-react-button-act-as-a-react-router-dom-link#:~:text=working%20with%20me%3A-,Just%20do%20like%20this%3A,-import%20Button%20from)
- [ ] [YT, Net Ninja - React Router 6 Tutorial | Upgrading from v5](https://www.youtube.com/watch?v=WfpmvgVZD1A)

## Know Your Docs

- [ ] [React Training Docs - Routes & Route](https://reactrouter.com/docs/en/v6/components/routes)
- [ ] [React Router Docs - Quick Start](https://reactrouter.com/docs/en/v6/getting-started/overview)
- [ ] [React Router Docs - React Router v6](https://reactrouter.com/docs/en/v6)
