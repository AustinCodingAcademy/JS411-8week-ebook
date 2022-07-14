# Authorization with Firebase

So far you've learned something about **Serverless Functions**(FireBase Cloud functions). You've sent data from the back end with **node** to the front end browser. We can do the same with our applications. Sending data back and forth from the front end react app to the back end is a very useful tool to have. Not all applications will need  **Serverless Functions** but, there is no way to accomplish certain tasks with out backend code. One of those tasks is **Authorization**.

**Authorization** needs to be done securely. If anyone can access your **Authorization** process and tokens it could compromise your app. Doing this server-side on the back end is much safer since everything is exposed on the front end.

## Authentication vs Authorization

Let's first clear up the definition of these two words. **Authentication** is the process of verifying whether a person-user has access to a server; are they a user?. It's like buying a ticket to a concert and flashing it at the gate(*sign-in*), then you get a wristband(*authenticated*) and you're allowed to go in and enjoy the music!

  > ...but what's a *backstage pass*?

When we build apps with data that needs to be allowed to certain person-users and restricted to others we need to implement **Authorization**. This is the process of assigning **roles** to each person-user.

Maybe you're building a classroom management app for you and your students. All of the data for this app will be stored in the same database and served by the same server but you don't want your students to have access to other students' grades and turned-in assignments but still have access to their own assignments and grades. However, for you, the teacher you want to be able to see all of the student's grades. To solve this problem you would assign each user of the app a role when they sign-up so each has specific levels of **authorization**. Teachers would get a `teacher` role, students would get a `student` role and maybe parents would get a `parent` role.

In your Express server you'd add an `if` statement to each route that asks if they are a `teacher` to access the resources behind the `getAllGrades()` so that `student` and `parent` users would be blocked from this particular resource.

  > ...**authorization** is a backstage pass. Beyond being admitted to the concert(**authentication**) you're also allowed to go backstage and maybe meet the artists!

	
## Setup Serverless Cloud Functions from FireBase with the Database

The following is a follow-along where you'll continue from the previous app you were working on in the **serverless** lesson.

1. Setup the config file so our app and database will connect with the local functions firebase emulator. 

Add:
`import { getFunctions,connectFunctionsEmulator } from 'firebase/functions';` 
Add:
`export const functions = getFunctions(app); connectFunctionsEmulator(functions, "localhost", 5001);`

=== "firebase-config.js"
```javascript
// firebase-config.js
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
import { getFirestore } from "@firebase/firestore";

import { getFunctions,connectFunctionsEmulator } from 'firebase/functions';

const firebaseConfig = {
  apiKey: process.env.REACT_APP_FIREBASE_KEY,
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

Add: `const admin = require('firebase-admin');`

Add: `admin.initializeApp();`
=== "functions/index.js"
```javascript
const functions = require("firebase-functions");
// Since we are writing in node we need to require('firebase-admin')
const admin = require('firebase-admin');
admin.initializeApp();


exports.helloWorld = functions.https.onRequest((request, response) => {
  functions.logger.info("Hello logs!", {structuredData: true});
  response.send("Hello from Firebase!");
});
```

## Authorization using Serverless Cloud Functions

Remember **Serverless Cloud functions** are just back end code. In our case it is **node**. We are going to use a combination of built in
methods and **node** to create a function that is callable on the front end. Again we are doing a very similar thing to any api you have called before. Except we are not using **fetch** or **axios**. We will be using built in firebase methods.

  > FireBase refers to roles as claims because they are meant to be used for roles and other purposes!

=== "functions/index.js"
```javascript
// require() statements ect...
// exports.helloWorld ect...

//Built in firebase methods sets up api end point for us to call
 exports.addAdminRole = functions.https.onCall(async (data,context) => {      
    try {
        const roles = {
            teacher: false,
            student: false,
        }
        roles[data.role] = true;
        // Tell our database to use data from our front end to
        // create a claim/role
        await admin.auth().setCustomUserClaims(data.uid, roles);

        // The next 3 lines for testing purposes to see what is happening
        const userData =  await admin.auth().getUserByEmail(data.email)
        console.log("userDatauserData",userData);
        return {result: userData} // Returning entire userData Object not 
        //necessary in production just userData.metadata or a "success" string  

    } catch (error) {
        console.log(error);
    // See https://firebase.google.com/docs/functions/callable#handle_errors
    }
})
```
#### Call the Cloud Function

Now We need to call the `addAdminRole` **Cloud function** on the front end when a user signs in so that they can be assigned a role. To do that we will add a `createRole` function to the file our user signs up and calls the `register` function.

  >Note: userCredential?.user is called [object chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/) enables you to read the value of a property located on an object without having to check that the property exists first. It will return `undefined` instead of crashing/throwing an error.

```javascript
// App.js
import React, { useState } from 'react';
import auth from './firebaseConfig';
import { createUserWithEmailAndPassword, signOut } from 'firebase/auth'

// Get our functions from the config file 
import {functions} from './../firebase-config';
//Firebase method to call our cloud function we setup
import { httpsCallable } from "firebase/functions";

////////////////////////
const createRole = async (userCredential,userRole) => {
  //httpsCallable() takes in our functions config and the name 
  //of the function in our functions/index.js we want to call
  const addAdminRole = httpsCallable(functions, 'addAdminRole');
  const email = userCredential?.user.email;
  const uid = userCredential?.user.uid;
  const role = userRole;
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
      //Invoke the createRole function
      //For now we will hard code the role
      //You will make it selectable programmatically in the assignment 
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
In order to run react and Sign up a new user and use the **cloud functions** you will need to run two terminals. In vscode click the Terminal menu and select New Terminal or press the + button in the terminal menu on the far right of the terminal. The first terminal will stay in the root directory. The second terminal should be in the functions folder `cd functions`. In the first terminal run your react app like normal `npm run start`. Then in the second terminal run the functions emulator `firebase emulators:start`.

Sign up a new user and look at the object under claims you will see that the user now has `teacher:true`. You should see the same on the backend and front end since we setup a console.log and return value. The next step is to check for the existence of the `teacher:true` in the user object. Then putting the correct check in areas you want to restrict to certain types of users. You will be setting that up in the next assignment. 



## Know Your Docs

- [ ] [FireBase - Call cloud functions](https://firebase.google.com/docs/functions/callable#web-version-9)
