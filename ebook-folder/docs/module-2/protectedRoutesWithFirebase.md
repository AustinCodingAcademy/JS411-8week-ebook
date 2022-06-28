## Firebase Authorization and Protected Routes

In one of the previous lessons, you learned about Protected Routes and used cookies to keep track of when a user is authenticated. The browser has many ways to store user data. You can right-click and use the inspect tool in our Chrome Browser, then go to the **Application** tab. Under storage you will see the many storage options, each with their own pros and cons. For example, cookies are fast and small simple strings. However, Firebase uses **[indexedDB]("https://web.dev/indexeddb/)** which is an asynchronous storage of objects indexed with a key.

When protecting routes, the concept of **cookies** and **indexedDB** is similar, just implemented differently in the code. Let's take a look at what that may look like. Open up your **learn-firebase** app from the previous lesson, and sign up a new user. When inspecting your console, look for the `console.log(auth.currentUser)` results. You should see an object holding data about the user that is currently signed in. We can also use the `Application` tool in our integrated terminal to see the results of our currently logged in user under the `indexedDB` section.

=== "Console Log Results"

    ![auth-console-log](../images/auth-console-log.png)

=== "indexedDb Results"

    ![small-biz-example-two](./../images/auth-indexedDb.png)

=== "How to see IndexedDb"

    ![small-biz-example-three](./../images/application-direction.png)
    >NOTE: If you do not see **Application** listed at the top of the integrated terminal, you will need to click on the drop down arrow to see more options.

<!--
```javaScript
// accessToken Stored in indexDB and passed around in your app via the auth object from firebase and used in your code for authorization by calling built in firebase functions
    {
      accessToken: "eyJhbGciOiJSUzI1NiIsImtpZCI6IjFhZWY1…"
      providerId:"firebase"
      displayName:null
      email:"testingme@gmail.com"
      metadata:{createdAt: "1654706061672", creationTime: "Wed, 08…"}
       // Many more properties...
    }
```
 -->

## Authentication State Observer - `onAuthStateChanged`

Firebase has a lot of awesome functions we can use from their library, and it makes our job as developers easier to implement authentication. We will be using `onAuthStateChanged` function from `firebase` to keep an eye/observe whether or not some has logged out, logged in, and if maybe we have some stored information in memory from a previous session. Let's take a look at how that works.

In your **How to Authenticate with Firebase** project from the previous lesson, add the following code to your App component. The function `onAuthStateChanged` is an observer that will fire when the user logs in or out. Also, remember that `useEffect` is called during the initial mounting of the component. That is how the observer is initially set. The user object is tracked in state and can be passed around your app to check for authorized access, just like the `checkAuth()` function from the previous lesson. Moreover, we only want to have one source of truth and active observer for our authentication so we need to be able to unsubscribe and disconnect the function from Firebase. The `onAuthStateChanged` returns an `unsubscribe` function we save to a variable called... `unsubscribe`. The useEffect hook will run `unsubscribe` as a [cleanup function]("https://blog.logrocket.com/understanding-react-useeffect-cleanup-function/) whenever the component unmounts, deleting the Firebase connection.

=== "Authentication - onAuthStateChanged"

    ```javascript
    import {  onAuthStateChanged } from 'firebase/auth'
    import React, {useState, useEffect} from 'react';

    function App() {
      const [user, setUser] = useState({});
      // ...all your previous code: state, register, logout, clear inputs etc...

      useEffect(()=> {
        const unsubscribe = onAuthStateChanged(auth, (currentUser) => {
            console.log("currentUser",currentUser);
            setUser(currentUser);
          });

        console.log("unsubscribe",unsubscribe);

        return unsubscribe // we only want 1 instance of the user connected to database
                // cleans up and disconnects listener function when component is unmounted
    }, [])
    ```

## What and How

Protected Routes will work the same way you have learned so far with 1 major difference. You see, we are passing in a user prop that comes from our App component's state. We get that from `onAuthStateChanged`.

Another small difference you will see is, we are using `!!user`. This is a [double bang](https://betterprogramming.pub/javascript-bang-bang-i-shot-you-down-use-of-double-bangs-in-javascript-7c9d94446054) and it is used when you want the falsey value of something. For example `!null` in the chrome console will be true. Since the user object will either be `null` or an object, we want to get the falsey value if the user is truly `null`. So we will use `!!null`, since it is easier to reason that we want a `null` value to represent false.

## Changing the `ProtectedRoutes` Code

I know this seems like a lot, and you may not completely understand it, and that is ok. Let's implement all these cool things we are talking about and maybe we can visualize these concepts a little better. Follow along with the example below and update your code accordingly.

**Let's begin with the `ProtectedRoute` component.**

=== "Protected Route Example - ProtectedRoute.js"

    ```javascript
    // "/components/ProtectedRoute.js"
    import React, { useContext } from "react";
    import { Route, Navigate } from "react-router-dom";

    export const ProtectedRoute = (props) => {
      // pass in user prop
      const { component: Component, user, ...rest } = props;

      return !!user ? <Component {...rest} /> : <Navigate to="/" />;
    };
    ```

- [ ] Navigate to your ProtectedRoute component `/component/ProtectedRoutes.js`
- [ ] In your destructured object that is coming from props, include the `user` property which will be passed down by it's parent container, our `Router`. _Next code block below_
- [ ] Instead of our `checkAuth()` function, we are simply going to check whether the `user` object, which is being passed down from the `onAuthStateChanged`, function is actually an object with data about the user, or the object is actually `null` and we do not have an authenticated user. We do this by checking the `!!` **double bang operator** we talked about earlier.

**Next, let's take a look at the `Router` component in our main `/src` directory.**

=== "Router Example - Router.js"

    ```javascript
      // ... import statements here...
      import {ProtectedRoute} from './components/ProtectedRoute';

      const Router = (props) => {
        const user = {props}; // pass as prop from App state via onAuthStateChanged
        return (
          <Routes>
              <Route exact path="/" component={Home} />
              <Route path='/about' element={<ProtectedRoute user={user} component={about} />} />
          </Routes>
        )
      }
      export default Router;
    ```

- [ ] Navigate over to your Router component in your main `src` directory
- [ ] We will destructure user from the user object being passed down from props, as we have done before.
- [ ] Last, just make sure you include that user as a property to be passed down to our `ProtectedRoute` component.

If you followed along correctly, the `<About />` component will be protected and only be shown based on some condition like authentication, after we add it in, of course. That's what we will be working on next!

## Additional Resources

- [ ] [YT, Web Dev Simplified - Firebase And Routing Context API Hook best practice](https://youtu.be/PKwu15ldZ7k?t=964)
- [ ] [Blog, Log Rocket - Understanding React’s useEffect cleanup function](https://blog.logrocket.com/understanding-react-useeffect-cleanup-function/)
- [ ] [Article, Medium - What is the Double bang (!!) operator in JavaScript?](https://javascript.plainenglish.io/what-is-double-bang-operator-in-javascript-90fc67ead5a4)
- [ ] [Article, web.dev - Working with IndexedDB](https://web.dev/indexeddb/)

## Know Your Docs

- [ ] [React Docs - Context API](https://reactjs.org/docs/context.html)
- [ ] [Firebase Docs - Set an authentication state observer and get user data](https://firebase.google.com/docs/auth/web/start#set_an_authentication_state_observer_and_get_user_data)
- [ ] [Firebase Docs - Auth Package](https://firebase.google.com/docs/auth/web/start#set_an_authentication_state_observer_and_get_user_data)
