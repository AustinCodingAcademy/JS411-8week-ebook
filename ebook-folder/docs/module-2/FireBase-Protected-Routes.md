
## FireBase authorization and protected routes

In one of the previous lessons you learned about protected routes. There you used cookies to track a user. The browser has many ways to store user data you can right click and inspect in chrome then go to the application tab and under storage  you will see the many storage options each with pros and cons. For example cookies are fast and small simple strings. However, firebases uses **indexedDB** which is an asynchronous storage of objects indexed with a key.

The concept of cookies and **indexedDB** for protecting routes is the same just different implementation in the code. Try it for your self open up your learn-firebase app from the previous lesson and sign up a new user and look at the `console.log(auth.currentUser)` or **indexdDB**. 

```javaScript
// accessToken Stored in indexDB and passed around in your app via the auth object from firebase and used in your code for authorization by calling built in firebase functions
    {accessToken: "eyJhbGciOiJSUzI1NiIsImtpZCI6IjFhZWY1…"
    providerId:"firebase"
    displayName:null
    email:"testingme@gmail.com"
    metadata:{createdAt: "1654706061672", creationTime: "Wed, 08…}
       // Many more properties...
    }
 

```
In your learn Firebase project add the following code to your App component. The function `onAuthStateChanged` is an observer that will fire when the user logs in or out. Also, remember that `useEffect` is called during mounting of the component. That is how the observer is initially set.  The user object is tracked in state and can be passed around your app to check for authorized access just like the `checkAuth()` function from the previous lesson. Moreover, we only want to have one source of truth and active observer for our authentication so we need to be able to unsubscribe and disconnect the function from Firebase. `onAuthStateChanged` returns a function that we return and will execute when the component unmounts and will delete the Firebase connection.   

```javaScript
import {  onAuthStateChanged } from 'firebase/auth'
import React, {useState, useEffect} from 'react';

function App() { 
const [user, setUser] = useState({});
//...All your previous code: state, register, logout, clear inputs ect...

useEffect(()=> {
const unsubscribe = onAuthStateChanged(auth, (currentUser) => {
    console.log("currentUser",currentUser);
    setUser(currentUser);
  });
  console.log("unsubscribe",unsubscribe);
  return unsubscribe // only want 1 instance of function running connected to database
            // cleans up and dissconects listener function when component is unmounted
}, [])
```

## What and How

Protected Routes will work the same way you have learned so far with 1 major difference. You see we are passing in a user prop that comes from our App component's state and we get that from `onAuthStateChanged`. 

Another small differnce you will see is we are using `!!user`. This is a [double bang](https://betterprogramming.pub/javascript-bang-bang-i-shot-you-down-use-of-double-bangs-in-javascript-7c9d94446054) and is used when you want the falsey value. For example `!null` in the chrome console will be true. Since the user object will either be `null` or an object we want to get the falsey value so we use `!!null` since it is easier to reason that we want a `null` value to represent false.

=== "Protected Route Example - ProtectedRoute.js"

```javascript
//"components/ProtectedRoute.js"
import React, { useContext } from "react";
import { Route, Navigate } from "react-router-dom";

  export const ProtectedRoute = (props) => {
      // passed in user prop
      const { component: Component,user, ...rest } = props;
  
      return ( 
        !!user ? ( <Component {...rest} /> ) : ( <Navigate to="/" /> )
      );
    };
```

### Use in code Code
=== "Router.js File with `ProtectedRoute` Function"

    ```javascript
      // ... import statements here...
      import {ProtectedRoute} from './components/ProtectedRoute';

      const Router = (props) => {
        const user = props.user; // comes from App state via onAuthStateChanged
        return (
          <Routes>
              <Route exact path="/" component={Home} />
              <Route path='/about' element={<ProtectedRoute user={user} component={about} />} />
          </Routes>
        )
      }
      export default Router;
    ```

Now, the `<About />` component will be protected and only be shown based on some condition like authentication, after we add it in, of course.


## Additional Resources

- [ ] [Firebase And Routing Context API Hook best practice](https://youtu.be/PKwu15ldZ7k?t=964)


## Know Your Docs

- [ ] [Context API](https://reactjs.org/docs/context.html)

