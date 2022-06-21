# Why firebase

Firebase is  a Backend-as-a-Service (BaaS) a google cloud service for developers to utilize all behind-the-scenes aspects of a web or mobile application so that they only have to write and maintain the frontend. Increasingly, more of software engineering complexity is moving from the back end to the frontend. Firebase allows all in one back end solution for Android, iOS, and the web so that all 3 can share 1 backend. Moreover, Firebase has a generous [free/demo](https://firebase.google.com/pricing) tier no charge if less than 1 gigabyte in storage. BaaS solutions are very attractive for companies. there are many BaaS services and FireBase is one of the most widely used ones. Example of some [companeis](https://blog.back4app.com/which-companies-use-firebase/) that use it. 

	

## How to use FireBase

 First create a new folder called learn-firebase in your dev folder and create a new react app there. Next, Sign up for [firebase](https://firebase.google.com/). You may have to create a google account if you do not have one. Remember The service is [free](https://firebase.google.com/pricing) upto 1 gigabyte in storage. 
- [ ] When you are signed in to your google account click the get started button on the main firebase page.
- [ ] Click the add project button and create a project name called learn-firebase then click continue.
- [ ] We will not use google analytics so leaving it on or off will not matter just leave it as default.
- [ ] From the drop down select Default Account For Firebase and press cerate project.
    * [ ] Follow the instructions in the README to complete then turn in.
- [ ] In the main firebase console page find the gear icon top left click it and select project settings
<!-- - [ ] Interview Questions: Blog to Show You Know -->
- [ ] Under Your apps you will see no projects and several icons click the one for web </>
- [ ] Under Register app Give your app a name then click register app.

. Once you are signed up for firebase and in the dashboard cli and recive a firebaseConfig object and use `npm i firebase`  to `import {initializeApp} from "firebase/app"`  and export it to any part that needs authentication and authorization. 


```javascript
   // firebase-config.js
    import { initializeApp } from "firebase/app";
    import {  getAuth } from 'firebase/auth'
    const firebaseConfig = {
    // config data from firebase here
    };
    const app = initializeApp(firebaseConfig);
    export const auth = getAuth(app);
```

The section bellow shows signing up a user for authentication in firebase. The data is stored on a cloud server based on the credentials you provide in the config file.
```javascript
import React, { useState, useEffect  } from 'react';
import { auth } from '../firebase-config';//credentials provided by firebase from above
import { createUserWithEmailAndPassword } from 'firebase/auth' // installed firebase dependency 

function SignUp() {
const [registerEmail, setRegisterEmail] = useState("");
const [registerPassword, setRegisterPassword] = useState("");

const register = async () => {
    try { 
    // TRY CATCH MUST USE WITH FIRE BASE ASYNC AWAIT FIRE BASE AUTHENTICATION
    const user = await createUserWithEmailAndPassword(
        auth,
        registerEmail,
        registerPassword
    );
    console.log(user);
    } catch (error) { // Give the user indication they need to try again and why
    // INVALID EMAIL
    // MiSSING PASSWORD
    // EMAIL EXISTS
    console.log(error.message);
    }
};

return (
    <div >
        <h3> Register User </h3>
        <input
        placeholder="Email..."
        onChange={(event) => {
            setRegisterEmail(event.target.value);
        }}
        />
        <input
        placeholder="Password..."
        onChange={(event) => {
            setRegisterPassword(event.target.value);
        }}
        />
        <button onClick={register}> Create User</button>
    </div>
);
}
export default SignUp;

    
```

## FireBase authorization and protected routes

In one of the previous lessons you learned about protected routes. There you used cookies to track a user. The browser has many ways to store user data you can right click and inspect in chrome then go to the storage tab you will see the many storage options each with pros and cons. For example cookies are fast and small simple strings. However, firebases uses indexedDB which is an asynchronous storage of objects indexed with a key. The concept of cookies and indexedDB for protecting routes is the same just different implementation in the code.

```javaScript
// Stored in indexDB and passed around and used in your code for authorization by calling built in firebase functions
    {accessToken: "eyJhbGciOiJSUzI1NiIsImtpZCI6IjFhZWY1…"
    providerId:"firebase"
    displayName:null
    email:"testingme@gmail.com"
    providerData:[{…}]
    metadata:{createdAt: "1654706061672", creationTime: "Wed, 08…}
    }
    // Many more properties just example

```

## .env

The .env file is for hiding sensetive information. The value can be accessed with the proccess.env object.

```javaScript
// .env 
// put in root directory
//
REACT_APP_FIREBASE_KEY="AIzaSyCHX8rJtQ234QpYF-SrLwE9VKr54uGNavb"

// fireBase-config 
// seperate file also in the root directory
const firebaseConfig = {
  apiKey: process.env.REACT_APP_FIREBASE_KEY,
  
};




```


Why are we learning about this? Well, protected routes and authentication are tools we can use to secure our app from unwanted guests. It's also a way to keep us logged in. You might have noticed last week that when we "logged in" to our app, everything was fine but when we refreshed the page we had to "log in" again. That's because the app had no way of understanding that we had an active session or cookie stored. Using protected routes and authentication will allow us to leave our machine (*computer*), come back the next day and open the app and remain right where we were when we left off. Only if our cookie has expired will we be required to log in again. Let's explore these processes further.

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-32-ProtectedRoutes - 411.2.4.1 -->
<iframe src="https://player.vimeo.com/video/492249128?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## What and How

First and foremost, what is a **Protected Route**? Just like the routes we worked with last class, these routes are protected by some logic. Think:

  > `if (userIsAuthorized) => go to profile; else {"Sorry, you're not authorized"}.`

It boils down to a bit of JavaScript logic that directs the user to one component or another based on some condition. It's easiest to show an example.

=== "Protected Route Example - Router.js"

    ```javascript
    const ProtectedRoute = ({component: Component, ...rest}) => {
      return (
        <Route
          // spread the rest of the props that are needed in this component
          {...rest}
          // define the value of the render method as a ternary that checks to see if checkAuth returns true or false
          render={(props) => checkAuth() === true
              // if true render the component with all the props
              ? <Component {...props} />
              // if false, use the Redirect component to update the url to `/login` so they are redirected to the login component
              : <Redirect to={{pathname: '/login', state: {from: props.location}}} />}
        />
      )
    }
    ```

So...that was pretty verbose. Let's make it a _little_ simpler:

=== "Simplified Protected Route Example - Router.js"

    ```javascript
    const ProtectedRoute = ({component: Component, ...rest}) => {
      return (
        <Route
        {...rest}
        render={(props) => checkAuth()
            ? <Component {...props} />
            : <Redirect to="/login" />}
        />
      )
    }
    ```

Ok now we can talk about what this is doing.

This `ProtectedRoute` function can accept any amount of props but the props we really want are the   and the `component` props from the route in question. On the first line...

`const ProtectedRoute = ({component: Component, ...rest}) => {`

...we "split" out the Component from the `rest` of the props in order to use it more easily later.

Next we return a `Route` component (from `'react-router'` package) and we send it the `...rest` of the components. Those could be things like `exact`, for example.

Then, we use the `render` function to determine what to show based on a conditions. We are referencing a custom-built `checkAuth()` function that we will create later. If `checkAuth` returns `true` then we will send the user on to the component they want to visit.

If `checkAuth` returns `false` then we will `Redirect` them to the `login` component so that they can log in.

  > NOTE: You don't have to remember all of this right now but know where to reference it. In the future when you are using protected routes (sometimes called **Private Routes**) you should be able to Google something like "React protected route" for an example.

### Where Do We Put this Code?

Where do we put this code?

We will put it in our `Router.js` file right above where the router is defined. And we use it by simply replacing one of the regular routes we've built already with this new `<ProtectedRoute>` that will route to a component that we want to be protected by authentication like this:

=== "Router.js File with `ProtectedRoute` Function"

    ```javascript
      // ... import statements here...

      const ProtectedRoute = ({component: Component, ...rest}) => {
        return (
          <Route
          {...rest}
          render={(props) => checkAuth()
              ? <Component {...props} />
              : <Redirect to="/login" />}
          />
        )
      }

      const Router = () => {
        return (
          <Routes>
              <Route exact path="/" component={Home} />
              <ProtectedRoute path="/about" component={About} />
          </Routes>
        )
      }
    ```

Now, the `<About />` component will be protected and only be shown based on some condition like authentication, after we add it in, of course.

### See It - Protected Routes

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-33-ImplementingProtectedRoutes - 411.2.4.2 -->
<iframe src="https://player.vimeo.com/video/492251808?color=2565EF&byline=0&portrait=0" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### The `checkAuth` Function

A very simple way to test if your protected route is working is build a dumb function like the one below:

`const checkAuth = () => true`

  > The code above will say that you are always logged in and anyone will be able to navigate to your protected route. **In production mode we generally want something more complicated than that.** 

Let's look at how to find a cookie from the **browser window**, shall we?

```javascript
  const checkAuth = () => {
      const cookies = cookie.parse(document.cookie)
      return cookies["loggedIn"] ? true : false
  }
```

Look closely at the function above, it's getting all of the cookies that exist on the browser and saying, "If there's one called `loggedIn`, return `true`. Otherwise return `false`. `cookie.parse` actually comes from the NPM package called [cookie](https://www.npmjs.com/package/cookie). We'll be installing it shortly. (Just make sure you do the following homework.) For now, let's assume if we're looking for a cookie called: loggedIn we probably put one, or set one, there called loggedIn with our app. This means our app can now save data to the local storage of a user's computer, or more specifically, their browser's local storage! This isn't something we've done yet.....ooooh....ahhhh.

## Cookies

<!-- ! Video Contents: Vimeo, Clayton@ACA - 411-34-CookiesAHighOverview - 411.2.4.3 -->
<iframe src="https://player.vimeo.com/video/492259264?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

Cookies are small bits of information that websites store on your browser. They are key-value pairs like objects but they only contain text. They help the browser make certain decisions using the content that's been stored in these cookies. That's exactly what we are going to do here.

You can interact with cookies at anytime by typing `document.cookie` in the console of your browser. Go ahead and do that now...

`document.cookie` + ++enter++ ==> `"ASPSESSIONIDAACDSPBS=IENHHCBEBANMBEPJNLICGFGP"` (or something like that)

If you did it should have brought back a string of characters that's hard to do anything with. This problem is solved with the [cookie package from npm](https://www.npmjs.com/package/cookie). It can be installed with the regular `npm i cookie` command.

Getting a list of our available cookies is easy with `cookie.parse`. Let's talk about setting cookies. In fact, you don't even need the cookie package to do this. You simply write:

`document.cookie = "loggedIn=true;max-age=60*1000"`

The `max-age` property decides how long the cookie will live for/be valid for. This property is counted in milliseconds so if you want the cookie to last one minute, you have to use `60*1000`, *(1000 milliseconds = 1 second; 1 second X 60 = 1 minute)*.

So now we've set this cookie on Login which means at Logout we'll want to clear it. *Keep this in mind as we move forward because we're going to continue working on the Login in portion for now.*

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

- [ ] [YT, freeCodeCamp.org - Protected Routes in React with React-Router](https://www.youtube.com/watch?v=Y0-qdp-XBJg)
- [ ] [Blog, Medium - Using Cookies in React, Redux, React-Router](https://rossbulat.medium.com/using-cookies-in-react-redux-and-react-router-4-f5f6079905dc)
- [ ] [Article, WhatAreCookies.com - What Are Cookies](http://www.whatarecookies.com/)

## Know Your Docs

- [ ] [React Training Docs - Redirects](https://reacttraining.com/react-router/web/example/auth-workflow)
- [ ] [NPM Docs - cookie](https://www.npmjs.com/package/cookie)
