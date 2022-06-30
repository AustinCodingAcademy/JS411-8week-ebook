# Protected Routes

_I arise full of eagerness and energy, knowing well what achievement lies ahead of me. —Zane Grey_

In the last lesson we learned how to route a user to a specific component/view based on the URL, but what if we needed to prevent certain users from seeing certain components. Let's say, if we had a class grading app we would want to prevent the students from seeing the `allGradesComponent` while still allowing the teacher to see it. We would put this `allGradesComponent` behind a **Protected Route** that will work like an if/else statement to see if the user is allowed to view it our not. Check it out below.

## Overview

Why are we learning about this? Well, protected routes and authentication are tools we can use to secure our app from unwanted guests. It's also a way to keep us logged in. You might have noticed last week that when we "logged into" our app, everything was fine but when we refreshed the page we had to "log in" again. That's because the app had no way of understanding that we had an active session or cookie stored. Using protected routes and authentication will allow us to leave our machine (_computer_), come back the next day and open the app and remain right where we were when we left off. Only if our cookie has expired will we be required to log in again. Let's explore these processes further.

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-32-ProtectedRoutes - 411.2.4.1 -->
<iframe src="https://player.vimeo.com/video/492249128?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

> NOTE=1: This video was recorded before React v18 and the rendering method for React is now `ReactDOM.createRoot()` which is imported from "react-dom/client".

> NOTE: This video was recorded before `react-router` & `react-router-dom` v6. We don't use `<Switch>` anymore, it is now `<Routes>`. Also, `<Redirect>` has been replaced by `<Navigate>`.

## What and How

First and foremost, what is a **Protected Route**? Just like the routes we worked with last class, these routes are protected by some logic. Think:

> `if (userIsAuthorized) => go to profile; else {"Sorry, you're not authorized, please log in."}.`

It boils down to a bit of JavaScript logic that directs the user to one component or another based on some condition. It's easiest to show an example.

=== "Protected Route Example without comments"

    ```javascript
    import { Navigate } from "react-router-dom";

    const ProtectedRoute = (props) => {

      const { component: Component, ...rest } = props;
      
      return (
        checkAuth() === true ? ( <Component {...rest} /> ) : ( <Navigate to="/login" /> )
      );
    };

    export default ProtectedRoute;
    ```

=== "Protected Route Example with comments"

    ```javascript
    // Import `Navigate` from react-router-dom
    import { Navigate } from "react-router-dom";

    // Create a component that takes props that will serve our Protected Routes
    const ProtectedRoute = (props) => {
      
      // Destructure the props passed to this component. 
      
      const { component: Component, ...rest } = props;
      
      /*  
      The ProtectedRoute function is going to take in props as an argument. 
      These props will contain, at the bare minimum, a component that will be rendered if the condition is met. Therefore, when we destructure the props we will say that the component to be rendered is the component being passed: `component: Component`
      
      See? We're taking the component that was passed...whatever it was and 
      storing it in a variable called `component` (lower-case c) so we can 
      `render()` it later by called `<Component />`

      Since React will expect all components to begin with a capital letter, 
      and the 'component' property is the prop that is storing the reference 
      to the `Component` we want to render, we simply rename `component` to 
      'Component` (upper-case C).
      
      Now we have a reference to what ever component was passed to this 
      `ProtectedRoute` functions i.e. `MySettings`, `MyAccount`, etc.

      The `{...rest}` of the properties we spread into a variable called `rest` 
      which uses the spread operator `...` to capture and give us a reference to 
      any remaining properties that may have been passed to this function. We 
      can then again reference `rest` when we need to pass those properties to 
      another Component down the chain.
      */
      
      return (
        // We will create this function `checkAuth()` soon, but for now, know
        // it returns either `true` or `false` depending on whether someone is
        // logged in or not.
        checkAuth() === true ? (
          // IF? "checkAuth()" returns `true`, render this Component. 
          // See? A component protected by some logic.
          <Component {...rest} />
        ) : (
          // ELSE: `checkAuth()` must be `false` and we want to "Navigate"
          // the user to the "/login" route by changing their URL using the
          // `Navigate` component from `react-router-dom`. The `to=` property
          // points to the path we want to replace the URL with: `"/login"`
          <Navigate to="/login" />
        )
      );
    };

    export default ProtectedRoute;
    ```

Let's talk about what this is doing:

- [ ] This `ProtectedRoute` component can accept any amount of props but the props we really want is the `component` property from the Route in question. On the first line...

> `const ProtectedRoute = ({component: Component, ...rest}) => {`

> ...we "split" out the Component from the `rest` of the props in order to use it more easily later.

- [ ] Next, we want to either return the `Component` or `Navigate` the user to the `Login` component. This will be based on a condition we will define. Think of your `checkForWin()` function in ticTacToe.

- [ ] We are referencing a custom-built `checkAuth()` function that we will create later. If `checkAuth` returns `true` then we will send the user on to the component they want to visit.

- [ ] If `checkAuth` returns `false` then we will `Navigate` them to the `login` component so that they can log in.

> NOTE: You don't have to remember all of this right now but know where to reference it. In the future when you are using Protected Routes (sometimes called **Private Routes**) you should be able to Google something like "React Protected Route" for an example.

### Where Do We Put this Code?

The `ProtectedRoute` component built above will be imported into our `Router.js` where we'll replace the `element=` prop of any `Route` we want to protect. 

=== "`Router.js` File with `ProtectedRoute` Function"

```javascript
import { Routes, Router } from "react-router-dom";
import Home from "./components/Home";
// #1 Import the component you want to be protected
import Dashboard from "./components/Dashboard";
// #2 Import the ProtectedRoute
import ProtectedRoute from "./components/ProtectedRoute";

const Router = () => {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route
        path="/dashboard"
        {/* #3 Replace the element prop with the ProtectedRoute and give the 
        component you want to be rendered as ITS element prop. */}
        element={<ProtectedRoute component={Dashboard} />}
      />
    </Routes>
  );
};

export default Router;
```

> NOTE: Notice how we are just sending the instance of the `Dashboard` component, this will be rendered by the Protected Route component based on the condition that someone is Authenticated or not. This does not need to be wrapped like a JSX element `<Dashboard />`. You need to simply pass in the `Dashboard` reference, from our import at the top of the file, as a property into our `ProtectedRoute` component.

Now, the `<Dashboard />` component will be protected and only be shown based on some condition like is the user authenticated, *after we add the checkAuth-functionality in*, of course.

We use the `ProtectedRoute` component by simply replacing the element property being rendered from one of the regular `Route`'s we've already built.

#### Changing a `Route` to a `ProtectedRoute`

For just a little more on this, let's look at them side by side, changing `Route` to a `ProtectedRoute`

We simply change this `Route` to a `ProtectedRoute` by changing the `element=` property(prop).

```javascript
// This
<Route path="/dashboard" element={<Dashboard />} />

// Becomes this
<Route path="/dashboard" element={<ProtectedRoute component={Dashboard} />}>
```

We pass in the `ProtectedRoute` component instead and make sure to include the component we just replaced with the `ProtectedRoute` as ITS `component=` prop.

> NOTE: The `<ProtectedRoute />` element can also take any properties you want to include, but we want to make sure to include the component we do want to render IF the user is Authenticated or "loggedIn".

### See It - Protected Routes

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-33-ImplementingProtectedRoutes - 411.2.4.2 -->
<iframe src="https://player.vimeo.com/video/492251808?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

> NOTE: This video was recorded before `react-router` & `react-router-dom` v6. We don't use `<Switch>` anymore, it is now `<Routes>`. Also, `<Redirect>` has been replaced by `<Navigate>`.

### The `checkAuth()` Function

A very simple way to test if your protected route is working is to build a dumb function like the one below:

`const checkAuth = () => true`

The code above will say that you are always logged in and anyone will be able to navigate to your protected route. **In production mode we generally want something more complicated than that. See [Protected Routes with Firebase lesson](./protectedRoutesWithFirebase.md).** Maybe when the person enters their email and password, our server app verifies they are who they say they are then sends a token to be stored as a cookie to prove they've been authenticated. From there, our front-end app could check to see if a valid cookie exists and allows the user to the protected component/view.

Let's look at how to find a cookie from the **browser window**, shall we?

=== "CheckAuth Function & NPM cookie"

```javascript
// With a special NPM Package called "cookie"
import cookie from "cookie";

const checkAuth = () => {
  const cookies = cookie.parse(document.cookie);
  return cookies["loggedIn"] ? true : false;
};
```

Look closely at the function above, it's getting all of the cookies that exist on the browser and saying, "If there's one called `loggedIn`, return `true`. Otherwise return `false`. `cookie.parse` actually comes from the NPM package called [cookie](https://www.npmjs.com/package/cookie). We'll be installing it shortly. (Just make sure you do the following homework.) For now, let's assume if we're looking for a cookie called: `loggedIn` we probably put one, or *set one*, there called `loggedIn` with our app. This means our app can now save data to the local storage of a user's computer, or more specifically, their browser's local storage! This isn't something we've done yet.....ooooh....ahhhh.

## Cookies

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-34-CookiesAHighOverview - 411.2.4.3 -->
<iframe src="https://player.vimeo.com/video/492259264?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

Cookies are small bits of information that websites store on your browser. They are key-value pairs like objects but they only contain text. They help the browser make certain decisions using the content that's been stored in these cookies. That's exactly what we are going to do here.

You can interact with cookies at anytime by typing `document.cookie` in the console of your browser. Go ahead and do that now...

`document.cookie` + ++enter++ ==> `"ASPSESSIONIDAACDSPBS=IENHHCBEBANMBEPJNLICGFGP"` (or something like that)

If you did this, it should have brought back a string of characters that's hard to do anything with. This problem is solved with the [cookie package from npm](https://www.npmjs.com/package/cookie). It can be installed with the regular `npm i cookie` command.

Getting a list of our available cookies is easy with `cookie.parse`. But first, let's talk about setting cookies. In fact, you don't even need the cookie package to do this. You simply write something like this in your browser console:

`document.cookie = "loggedIn=true;Max-Age=60*1000"` + ++enter++

The `Max-Age` property decides how long the cookie will live for/be valid for. This property is counted in milliseconds so if you want the cookie to last one minute, you have to use `60*1000`, _(1000 milliseconds = 1 second; 1 second X 60 = 1 minute)_.

In React & Node world, we can use the `cookie` package to write simple cookies as well. It will look something like this:

=== "Setting cookies using the `cookie` package"

```javascript
import cookie from "cookie";
// Or
// const cookie = require("cookie");

// Set a new cookie
document.cookie = cookie.serialize("loggedIn", "true", { maxAge: 1000 * 60 });

// Delete a cookie
document.cookie = cookie.serialize("loggedIn", null, { maxAge: 0 });

// To check your new cookies
console.log(cookie.parse(document.cookie));
```

The `cookie.serialize()` method takes in 3 parameters: the `key`, the `value`, then an Object that takes in some key/value pairs as options. The list of options when using the `cookie` package can be found [here]("https://www.npmjs.com/package/cookie#:~:text=//%20foo%3Dbar-,Options,-cookie.serialize%20accepts").

Setting the `maxAge` attribute to 0, or a negative number, will delete the cookie from memory.

So now we've set this cookie on Login which means at Logout we'll want to clear it. _Keep this in mind as we move forward because we're going to continue working on the Login in portion for now._

> NOTE: Without the `cookie` package, we would need to do some extra work in order to get our cookies to be more readable and usable. By default, `document.cookie` will return a concatenated string with all our key/values separated by a semi-colon. This makes it hard for us to extract the right bit of information we need. The npm package, `cookie`, simplifies that process for us, making it more practical.

Lets take a look at what it looks like to get a cookie without that `cookie` package.

=== "Cookies without NPM cookie - without comments"

    ```javascript
    document.cookie = "loggedin=true;Max-Age=1000*60";
    document.cookie = "anotherKey=anotherValue;Max-Age=1000*60";

    let cookies = {};

    document.cookie.split(";").forEach((el) => {
      let keyValue = el.split("=");
      return (cookies[keyValue[0]] = keyValue[1]);
    });
    ```

=== "Cookies without NPM cookie - with comments"

    ```javascript
    // Set some cookies
    document.cookie = "loggedin=true;Max-Age=1000*60";
    document.cookie = "anotherKey=anotherValue;Max-Age=1000*60";

    // Create an object called `cookies` which will be used to store our 
    key/values AFTER we break them down
    let cookies = {};

    // Get cookies by calling to the cookie method on the document: 
    //  "document.cookie"
    document.cookie // "loggedin=true;anotherKey=anotherValue

      // Split that concatenated string of joined key/values at the semicolons 
      //  and place it into an array
      .split(";") // returns ["loggedin=false", "anotherKey=anotherValue"]

      // For each element in our new Array of strings
      .forEach((el) => {
        // Split the element AT the "equal" sign
        let keyValue = el.split("="); // ["loggedin", "false"]

        // And for every element, we return a new key/value pair and attach it 
        // to our cookies object we create first
        return (cookies[keyValue[0]] = keyValue[1]);
        // At the end we get an object with 2 key values, which is much easier 
        // to work with: 
        // {loggedin: "true", anotherKey: "anotherValue"}
      });
    ```

Want to know more about cookies and what you can do with them? Read this very [detailed article on What Are Cookies](http://www.whatarecookies.com/).

## Practice It

<!-- ! Video Contents: CodeSandbox, ProtectedRoute Practice -->
<iframe src="https://codesandbox.io/s/yjzyzr29ov?from-embed=&file=/example.js"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="vigorous-gauss-pw0wb"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>

### Practice Section Instructions

- [ ] Open the sandbox above
- [ ] Navigate to the `Route.js` file and look at the comments
- [ ] Create a `ProtectedRoute` function where the commented line indicates
- [ ] Replace the use of `Route` with `ProtectedRoute` in the `<Switch>` component
- [ ] Do you see the components showing up?
- [ ] Use the address bar to navigate to the `"/about"` and `"/info"` pages. Do you see those?
- [ ] Replace the `true` with `false` in the `checkAuth` function. Are the components still showing up?

## Additional Resources

- [ ] [YT, Coding Addict - React Router 6 - Protected Route](https://www.youtube.com/watch?v=Y0-qdp-XBJg)
- [ ] [YT,Bro Code - WTF is a JavaScript "cookie"? 🍪](https://www.youtube.com/watch?v=i7oL_K_FmM8)
- [ ] [Article, WhatAreCookies.com - What Are Cookies](http://www.whatarecookies.com/)

## Know Your Docs

- [ ] [React Training Docs - Navigate ](https://reactrouter.com/docs/en/v6/components/navigate)
- [ ] [NPM Docs - cookie](https://www.npmjs.com/package/cookie)
