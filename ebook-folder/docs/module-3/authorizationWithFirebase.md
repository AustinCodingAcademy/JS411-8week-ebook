# Authorization with Firebase

Now that we've learned how to use **Serverless Functions**(FireBase Cloud functions) to pass data back and forth between our front-end and back-end let's see another way we can use them. Not every application you will need  **Serverless Functions** but, if it involves **Authorization** it will!

**Authorization** needs to be done securely, aka without being seen. If anyone can access your **Authorization** process it would compromise your app. Doing this server-side/on the back-end is much safer since everything is exposed on the front-end.

> NOTE: Before we begin, remember **Authentication** is the verification of a person being the person they say they are while **Authorization** is the level of access a person has. Think of the door signs that say *"Authorized Personnel Only"*.
	
## Setup Connect Serverless Functions to DB

The following is a follow-along where you'll continue from the previous app you were working on in the [**serverless functions** lesson](./serverless.md).

1. Setup the config file so our app and database will connect with the local firebase functions emulator. 

  - [ ] Add: `import { getFunctions,connectFunctionsEmulator } from 'firebase/functions';` 
  - [ ] Add: `export const functions = getFunctions(app); connectFunctionsEmulator(functions, "localhost", 5001);`

  ```javascript
  // firebase-config.js
  import { initializeApp } from "firebase/app";
  import { getAuth } from "firebase/auth";
  import { getFirestore } from "@firebase/firestore";

  import { getFunctions,connectFunctionsEmulator } from 'firebase/functions';

  const firebaseConfig = {
    APIKey: process.env.REACT_APP_FIREBASE_KEY,
    authDomain: process.env.REACT_APP_FIREBASE_DOMAIN,
    projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
    storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
    messagingSenderId: process.env.REACT_APP_FIREBASE_SENDER_ID,
    appId: process.env.REACT_APP_FIREBASE_APP_ID,
    measurementId: process.env.REACT_APP_FIREBASE_MEASUREMENT_ID,
  };

  const app = initializeApp(firebaseConfig);
  export const auth = getAuth(app);
  export const db = getFirestore(app);

  // Import and connect the functions to the app and specify the localhost port
  export const functions = getFunctions(app);
  connectFunctionsEmulator(functions, "localhost", 5001);
  ```

2. In the `functions/index.js` file we are going to connect our **cloud functions** to the administration controls of the database.

  - [ ] Add: `const admin = require('firebase-admin');`

  - [ ] Add: `admin.initializeApp();`

  ```javascript
  // functions/index.js
  const functions = require("firebase-functions");
  // Since we are writing in Node.js we need to require('firebase-admin')
  const admin = require('firebase-admin');
  // then run its initialize method
  admin.initializeApp();


  exports.helloWorld = functions.https.onRequest((request, response) => {
    functions.logger.info("Hello logs!", {structuredData: true});
    response.send("Hello from Firebase!");
  });
  ```

## Authorization Using Serverless Cloud Functions

Remember **Serverless Cloud functions** are just back-end code. In our case it's **Node.js**. We are going to use a combination of built in methods and **Node.js** to create a function that is callable from the front-end. Again we are doing a very similar thing to any API you have called before *except* we are not using **fetch** or **axios**; we'll be using built in FireBase methods.

  > FireBase refers to roles as "**claims**" because they are meant to be used for roles and... other purposes!

```javascript
// functions/index.js
// import and require() statements ect...
// exports.helloWorld ect...

// Built in FireBase methods set up an API end-point for us to call
 exports.addAdminRole = functions.https.onCall(async (data,context) => {      
    try {
        const roles = {
            teacher: false,
            student: false,
        }
        roles[data.role] = true;
        // Tell our database to use data from our front-end to
        // create a claim/role
        await admin.auth().setCustomUserClaims(data.uid, roles);

        // The next 3 lines for testing purposes to see what is happening
        const userData =  await admin.auth().getUserByEmail(data.email)
        console.log("userDatauserData",userData);
        return {result: userData} // Returning entire `userData` Object isn't 
        // necessary in production; just return userData.metadata or a 
        //  "success" string.

    } catch (error) {
        console.log(error);
    // See https://firebase.google.com/docs/functions/callable#handle_errors
    }
})
```

## Call the Cloud Function

Now We need to call the `addAdminRole` **Cloud function** on the front-end. When a user signs in they can be assigned a role. To do that we will add a `createRole` function in the file where our user signs up and invokes the `register` function.

  > Note: Below `userCredential?.user` is using [object chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/) it enables you to read the value of a property located on an object without having to check if the property exists first. If the property doesn't exist it will return `undefined` instead of crashing the app or throwing an error.

```javascript
// App.js
import React, { useState } from 'react';
import auth from './firebaseConfig';
import { createUserWithEmailAndPassword, signOut } from 'firebase/auth'

// Get our functions from the config file 
import {functions} from './../firebase-config';
// Firebase method to call our cloud function we setup
import { httpsCallable } from "firebase/functions";

////////////////////////
const createRole = async (userCredential,userRole) => {
  // `httpsCallable()` takes in our functions config and the name 
  //   of the function in our `functions/index.js` we want to call.
  //    It then returns a function for us to use.
  const addAdminRole = httpsCallable(functions, 'addAdminRole');
  const email = userCredential?.user.email;
  const uid = userCredential?.user.uid;
  const role = userRole;
  // Our Serverless cloud function we made expects an object
  //   with the user `id` the users email and the role they will be assigned
  const result = await addAdminRole({uid, email,role})
  console.log("result",result);
}
/////////////////////////
function App() {
  const [registeredEmail, setRegisteredEmail] = useState("");
  const [registeredPassword, setRegisteredPassword] = useState("");

  const register = async () => {
    try { 
      const user = await createUserWithEmailAndPassword(
          auth,
          registeredEmail,
          registeredPassword
      );
      // Invoke the `createRole` function.
      // For now we will hard code the role. You will make it selectable 
      //  programmatically in the upcoming assignment 
      createRole(user, 'teacher');

    } catch (error) { 
      console.log(error.message);
      clearForm()
    }
  };

  const logout = async () => {
    await signOut(auth);
  };

  const clearForm = () => {
    document.getElementById("user-form").reset()
  }
  return (
    <div >
      <h3> Register User </h3>
      <form id="user-form" >
        <input
          placeholder="Email..."
          onChange={(event) => {
              setRegisteredEmail(event.target.value);
          }}
        />
        <input
          type="password"
          placeholder="Password..."
          onChange={(event) => {
              setRegisteredPassword(event.target.value);
          }}
        />
        <button onClick={register}> Create User</button>
        <button onClick={logout}> Sign Out </button>
      </form>  
    </div>
  ); 
}

export default App;
```
### Run and Test

To sign-up a new user we need both our front-end(React app) and our Serverless function simultaneously running. In order to **locally** run React and these **cloud functions** both at the same you will need to run two terminals at the same time. 

  - [ ] In VSCode click the Terminal menu and select New Terminal.
  - [ ] Alternatively, press the + button at the top of your terminal emulator to create a new session.
  - [ ] The first terminal will stay in the root directory to run your React app: `npm run start`
  - [ ] The second terminal should be in the functions folder: `cd functions` then `firebase emulators:start`.
  - [ ] Sign up a new user and look at the object under claims. You'll see that the user now has `teacher:true`. You should see the same on the back-end and front-end since we setup a `console.log` statement and return value. 

The next step is to check for the existence of the `teacher:true` in the user object. Then putting the correct check in areas you want to restrict to certain types of users. You will be setting that up in the next assignment. 

## Know Your Docs

- [ ] [FireBase - Call Cloud Functions](https://firebase.google.com/docs/functions/callable#web-version-9)
