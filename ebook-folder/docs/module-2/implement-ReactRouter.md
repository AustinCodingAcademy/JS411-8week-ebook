# Implementing React-Router

## Overview

Now that you've gotten a hold of this new tool and have an understanding of why and when to use it, let's take some time to see how it's implemented so you can really get the flow of these "wrapper"/higher-order components.

## Implement BrowserRouter

=== "Implement BrowserRouter Video"

    <!-- ! Video Contents: Vimeo, Clayton@ACA - 411-29-ImplementingBrowserRouter - 411.2.3.1 -->
    <iframe src="https://player.vimeo.com/video/492232669?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

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

=== "Video Outline"

    - [ ] Create `Router.js file`
    - [ ] import `react`, `switch`, & `Route`
    - [ ] Import the two components you want to test with!!!

    - [ ] `import React from 'react'`
    - [ ] `import { Switch, Route } from 'react-router'`
    - [ ] `import Home from './Home'`
    - [ ] `import App from './App'`
    - [ ] Create Router function/component:

      ```javascript
        const Router = () => {
          return (
              <Switch>
                  <Route path="/home" component={Home} />
                  <Route path="/app" component={App} />
              </Switch>
          )
        }
      ```

    - [ ] `export default Router`
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

    - [ ] 6. Use a Material-UI Button... `import Button from '@material-ui/core/Button'`



      ```javascript
        <Link to="/home"> */}

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

## Practice It

<!-- ! Video Contents: CodeSandBox - React Router Basics -->
<iframe src="https://codesandbox.io/embed/yjzyzr29ov?fontsize=14&hidenavigation=1&theme=dark"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="React Router - Basic"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>

### Practice Section Instructions

- [ ] Open the code editor and navigate to `example.js` on the left-hand side
- [ ] At the bottom of the file `example.js` (but before the export, line 79 or 80), create a new functional component called Urls
- [ ] The `Urls` component should return the following:

  ```html
    <div>
        <h3>URLs Page</h3>
        <ul>
            <li><a href="https://www.google.com">Google</a></li>
            <li><a href="https://www.facebook.com">Facebook</a></li>
            <li><a href="https://www.amazon.com">Amazon</a></li>
        </ul>
    </div>
  ```

  > NOTE: Try not to copy/paste this code. It's good to practice writing it.

- [ ] Add the `Urls` component into the `Router` with a path of `/urls` just below `{Home}`, `{About}`, and `{Topics}` on line 25.
- [ ] Add a `Link` for this component as well, starting at line 18, that goes `to` `/urls`.
- [ ] Refresh the browser and click on the link to the `Urls` component. You should see your new component.

## Additional Resources

- [ ] [YT, Dev Ed - React Router Tutorial | React For Beginners](https://www.youtube.com/watch?v=Law7wfdg_ls)
- [ ] [Reference, GitHub React Training - Link](https://github.com/ReactTraining/react-router/blob/master/packages/react-router-dom/docs/api/Link.md)

## Know Your Docs

- [ ] [NPM Docs - React-Router](https://www.npmjs.com/package/react-router)
- [ ] [React Training Docs - React-Router](https://reacttraining.com/react-router/)
