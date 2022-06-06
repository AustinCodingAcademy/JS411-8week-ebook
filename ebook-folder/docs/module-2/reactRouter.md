# Intro to React Router

*The glow of one warm thought is to me worth more than money. —Thomas Jefferson*

## Overview

What we've learned so far is great. It helps us build a dynamic single-page application (SPA), but so far our app literally just has one page. What if we want it to have more than one? Like a sign-up page, contact us page, products page, whatever!! That's where React Router comes in. With React Router we can control the URL in the address bar and tell our server to return the file that matches the URL we just changed it to.

For instance: "www.mywebsite.com/contactus" might return the "Contact Us" page whereas "www.mywebsite.com/signup" might return the "Sign Up" page.

Continue on to get the low down on how to make this work.

## Why

Why use React Router? As we mentioned above, we use React Router to help us handle multiple routes in our URL. For example, every time you spin up your music dashboard app using `npm start` it sends the browser to the default path of the application in your computer `~/devFolder/musicApp/`, or simply, `~/`. Through the local port 3000 it shows up in your browser as "http://localhost:3000/" . But later, when we add a users page and want the route `/users` registered with our app's Router so the browser will navigate to the Users component that we built, we use React Router. Thus, we will have the following paths match the following components:

* `/` -> HomePage Component
* `/users` -> Users Component
* `/users/0` -> UserDetails Component with the details of our first user

=== "React Router: The High Overview"

    <!-- ! Video Contents: Vimeo, Clayton@ACA - 411-28-ReactRouterHighOverview - 411.2.3.1 -->
    <iframe src="https://player.vimeo.com/video/492225296?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

=== "Video Breakdown"

    - [ ] App Demo
    - [ ] What's going on
    - [ ] How?
    - [ ] Process
    - [ ] Tools Used
    - [ ] react-router-dom
    - [ ] react-router
    - [ ] Overview of components - (floating around able to be called by anyone)
    - [ ] Go to index.js to see `<App />` being called
    - [ ] How to manage the shift between the two <App /> & <Home />
    - [ ] Flow of functions in the functional programming heap of React-Router...
    - [ ] `reactDOM.render()`
    - [ ] `<Main />`
    - [ ] `<BrowserRouter />`
    - [ ] `<Router />`
    - [ ] `<Routes />`
    - [ ] `<Route path="/mycomponentofchoice" component={MyComponentOfChoice} />`
    - [ ] `<MyComponentOfChoice />`
    - [ ] `<Link to="/mycomponentofchoice" />`
    - [ ] Go to docs and install npm packages
    - [ ] Installation
    - [ ] `npm i react-router react-router-dom`
    - [ ] Open up the React Router Docs: [https://reactrouter.com/web/guides/quick-start](https://reactrouter.com/web/guides/quick-start)

> VIDEO-NOTE-1: This video was recorded before React Router v6. We don't use `<Switch>` anymore. It is now `<Routes>`

> VIDEO-NOTE-2: This video was recorded before React v18 and the rendering method for React is now ReactDOM.createRoot() which is imported from "react-dom client". See code snippet below.

```javascript
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

> VIDEO-NOTE-3: With React Router v6, you'll only import tools(functions) from `react-router-dom` not `react-router`.

## What

### Install the Router Packages

So how do we integrate React Router into our code? It's actually quite simple . . . it's an NPM package just like Material UI! Who would have thought?!? To install it in our project we just run the command `npm i react-router react-router-dom` inside our React app. This command installs two packages, as you may have noticed, react-router and react-router-dom. Go ahead and do that in your music app.

It should be noted at this point that all forms of building front-end applications will need the use of a "router" of some shape and form. If you were building with Angular you'd need to use [Angular's RouterModule and Routes](https://angular.io/guide/router). If you were building with Vue you'd need to use [Vue Router](https://router.vuejs.org/). They all do the same job in their respective stacks, so while we're learning to build with React, let's use [React Router](https://reacttraining.com/react-router/).

### Creating the Router

After installing the libraries/packages that make up the magic of React Router, we need to create a router, which really is just a function that, when called, returns the component it's assigned to. We start by creating a file called `Router.js`, usually right inside the `src/` folder. Here's an example of a simple Router file:

=== "`src/Router.js`"

    ```javascript
    import React from 'react';

    // Here is where we are importing to the two main components we need from the React Router package.
    import { Routes, Route } from 'react-router-dom';

    // Local imports. Import components we built ourselves
    import Home from './Home';
    import Dashboard from './components/Dashboard';
    import Profile from './components/Profile';

    const Router = () => {
        return (
            { /* Then we use Routes and Route. Routes acts like a regular JS Switch* Statement */ }
            <Routes>
                { /* depending on the path in the URL, one of these Routes will be returned and their component rendered */ }
                <Route path="/*" element={<Home/>} />
                <Route path="/dash" element={<Dashboard/>} />
                <Route path="/user/:id" element={<Profile/>} />
            </Routes>
        );
    }

    //Don't forget to export your newly create Router component
    export default Router;
    ```

    > NOTE: When using the `*` at the end of a path it means to match deeply or exactly. We can only use `*` at the end of a path, make sure to never use it at the start or middle of a path(security errors will occur). You'll only need the trailing `*` when there is another `<Routes>` somewhere in that route's descendant tree. In that case, the descendant `<Routes>` will match on the portion of the pathname that remains.

The `Routes` component always wraps multiple `Route`'s, so it is the single parent container this component returns. The `Route`'s are relative and help with leaner and more predictable code. `Route`'s are chosen based on the best match, not in order. You can put your `Route`'s in any order you like, the router will detect the best route for the current URL automatically. For readability if you want to start with "home" thats fine but nothing to worry about if you don't.

  > NOTE: As we customize the "Router" component, keep in mind the `Routes` component bares an obvious resemblance in appearance and functionality to the [`switch() { case: }`](https://www.w3schools.com/js/js_switch.asp). 

In summary, `Routes` is telling the application, "hey, look at all of the paths in this section to see if the current path in the browser matches any of these. If so, return the route that's connected to it."

The `Route` then, is a component which specifies a combination of the correct relationship of "path" and "component". If the URL in the browser matches the path, then the Route sends the application to the correct component. In this case, `/dash` will load up the Dashboard component. You see the `<Route>` is the `case:` statement that says to do this when this is the case.

=== "Remember to Import the Components You Want to Use"

    ```javascript
    // You need to use the Home component in the Route component you must import the Home component first
    import Home from './Home'

    <Routes>
        <Route path="/" element={<Home/>} />
    </Routes>    
    ```

This might seem obvious but it's an important piece to remember. Each of the components you want to use in your Router have to be imported so they're available/registered with the Router component. Also, notice that we used the Home component as the default route. If we're using Router we have to create a default case for the `<Routes>` component to return, **because ALL components in React must return something**!!!

### Rendering What Comes out of the Router

Great, so we've created our Router file. Now what? Let's tell the application to use it! Remember, we created the file but haven't made the other parts of the application aware of it. The very first file of our app, the `index.js` file is our entry point into the app. Go to it and find the component it's currently using, which is most likely `<App />`. We're going to make some renovations. Look below at the default setup of our app.

=== "Basic React `index.js` File"

    ```javascript
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import './index.css';
    import App from './App';
    import reportWebVitals from './reportWebVitals';

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
        <React.StrictMode>
            <App />
        </React.StrictMode>
    );
    // If you want to start measuring performance in your app, pass a function
    // to log results (for example: reportWebVitals(console.log))
    // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
    reportWebVitals();
    ```

  > NOTE: Don't worry about the `reportWebVitals` part. It is an API which we can learn to use later. Just focus on the steps ahead.

As you probably guessed, we have to import things . . .The first (#1) is `BrowserRouter`. This, aptly named, package navigates the browser where we want it to. The second (#2) step we have to import is the `Router` component we just finished building.

=== "React `index.js` File with `BrowserRouter` & Our `Router` imported"

    ```javascript
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    // #1
    import { BrowserRouter } from 'react-router-dom';
    import './index.css';
    import App from './App';
    import reportWebVitals from './reportWebVitals';
    // #2
    import Router from './Router';

    // ...more code below here...
    ```

  > NOTE: The order in which packages and components are imported is not important to the app. The order is only important to you and your team, so find a style you like and develop it. In the example above you'll see package dependencies listed first, then styles, then components.

Next, or **#3**, we have to create a component to return this stuff for us. Let's call it `Main` and have it return `<BrowserRouter>`. Then stick our `<Router />` component inside of it. This "sticking" inside is actually called "wrapping". We "wrap" the `<BrowserRouter>` around the `<Router>` so our **entire** application is encapsulated by the `<BrowserRouter>`.

=== "Newly Created `Main` Component in the `index.js` File"

    ```javascript
    // ...more code above here...
    import Router from './Router';

    const root = ReactDOM.createRoot(document.getElementById("root"));

    // #3
    const Main = () => (
    <BrowserRouter>
        <Router />
    </BrowserRouter>
    );

    root.render(<App/>);

    // ...more code about service worker blah blah below here...
    ```

The **fourth(#4) step** is to use the "wrap". To do this we'll pass the `Main` component we just built to the `root.render()` method. Now our app's `index.js` file should look like this:

=== "Replaced `<App />` with `<Main />`"

    ```javascript
    import React from 'react';
    // #1
    import ReactDOM from 'react-dom';
    import { BrowserRouter } from 'react-router-dom';
    import './index.css';
    import reportWebVitals from "./reportWebVitals";
    // We no longer need our App component to be imported here...
    // #2
    import Router from './Router';

    const root = ReactDOM.createRoot(document.getElementById("root"));

    // #3
    const Main = () => (
        <BrowserRouter>
            <Router />
        </BrowserRouter>
    );

    // #4
    root.render(<Main/>);

    // If you want to start measuring performance in your app, pass a function
    // to log results (for example: reportWebVitals(console.log))
    // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
    reportWebVitals();
    ```

We call this "wrapping" stuff **Higher Order Components** or **HOCs** because, just like the Higher Order functions (`.map`, `.reduce`, `.filter`) you learned in 211, they take functions as their arguments and sometimes return functions: `root.render()` takes in `Main` which returns `BrowserRouter` which returns `Router` with returns one of the `Routes` which returns its appropriate component which then returns the JSX so the `render` can plug it into the DOM inside an element with the `id` `"root"`.

> **Get it?** If not, walk through that again slowly. Draw it out.

### Notes on this React Router/BrowserRouter stuff:

1. Be sure to `import { BrowserRouter } from 'react-router-dom'`, **Step 1**

2. It is key that this `{ BrowserRouter }` wraps our application because it is needed for the communication between our browser and our Router component. Additionally, when we take a look a the React `Link` component (coming up) we will learn that `Link`s can only be used inside of a "router" which `BrowserRouter` takes care of for us.

    > Please note: You don't have to understand that right now, just start recognizing the pattern we are using above. Components return components that return components or, more simply, a function returns a function that returns a function. Functional programming!

3. Remember to import your custom Router component, `import Router from './Router'` so it can be used in the `index.js` file, **Step 2**.

4. In **Step 3**, we created a small component function called `Main` (you can call it something else if you like) and we wrapped our `<Router />` inside the `<BrowserRouter> </BrowserRouter>` tags so the `BrowserRouter` component returns it.

You may be thinking, "couldn't we have just done that in the Router file?". Yes, but this pattern will allow you to eventually add components around the router that you want to see on every page. For example, a `Header` and `Footer` component, like you see below:

=== "Example of `Main` Component"

    ```javascript
        const Main = () => (
            <BrowserRouter>
                {/*You can use basic HTML elements to wrap your custom components so that you are in line with conventional semantic structural practices*/}
                <header>
                    <HeaderComponent />
                </header>

                <main>
                    <Router /> {/* <-- See? Your different routes can be render here while still keeping the Header and Footer the same */}
                </main>
                
                <footer>
                    <FooterComponent />
                </footer>
            </BrowserRouter>
    )
    ```

    > But do NOTE that you may see slightly different patterns in other tutorials and that's perfectly fine. While you're learning, let's stick with this pattern. You can explore and diverge later on.

5. **Step 4** is simply replacing the call to `App` in `root.render` with the new `Main` function we just created. Once this step is done you should be able to load up your application and switch between the `Home` and `Dashboard` components by typing the corresponding URL in the browser. But of course, typing in that URL is annoying and you're definitely not asked to do that on anyone else's web site. To fix this let's learn how to use the `Link` part of React Router which is a programmatic way to switch the browser URL.

## Know Your Docs

- [ ] [w3S Docs - Switch Statement](https://www.w3schools.com/js/js_switch.asp)
- [ ] [w3S Docs - React Router](https://www.w3schools.com/react/react_router.asp)
- [ ] [React Training Docs - React Router](https://reacttraining.com/react-router/)
- [ ] [React Router Docs - Quick Start](https://reactrouter.com/docs/en/v6/getting-started/overview)
- [ ] [React Router Docs - React Router v6](https://reactrouter.com/docs/en/v6)
- [ ] [React Router Docs - Upgrading from v5](https://reactrouter.com/docs/en/v6/upgrading/v5)
