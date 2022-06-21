# Why firebase

Firebase is a Backend-as-a-Service (BaaS) a google cloud service for developers to utilize all behind-the-scenes aspects of a web or mobile application so that they only have to write and maintain the frontend. Increasingly, more of software engineering complexity is moving from the back end to the frontend. Firebase allows all in one back end solution for Android, iOS, and the web so that all 3 can share 1 backend. Moreover, Firebase has a generous [free/demo](https://firebase.google.com/pricing) tier no charge if less than 1 gigabyte in storage. BaaS solutions are very attractive for companies. there are many BaaS services and FireBase is one of the most widely used ones. Example of some [companeis](https://blog.back4app.com/which-companies-use-firebase/) that use it. 

	

## How to use FireBase

 First create a new folder called learn-firebase in your dev folder and create a new react app there. Next, Sign up for [firebase](https://firebase.google.com/). You may have to create a google account if you do not have one. Remember The service is [free](https://firebase.google.com/pricing) upto 1 gigabyte in storage. 

- [ ] Install firebase into your node_modules and add it to package.json `npm i firebase` 
- [ ] When you are signed in to your google account click the get started button on the main firebase page.
- [ ] Click the add project button and create a project name called learn-firebase then click continue.
- [ ] We will not use google analytics so leaving it on or off will not matter just leave it as default.
- [ ] From the drop down select Default Account For Firebase and press cerate project.
    <!-- * [ ] Follow the instructions in the README to complete then turn in. -->
- [ ] In the main firebase console page find the gear icon top left click it and select project settings
<!-- - [ ] Interview Questions: Blog to Show You Know -->
- [ ] Under Your apps you will see no projects and several icons click the one for web </>
- [ ] Under Register app Give your app a name then click register app and SAVE ALL the code for later in a file called firebaseConfig! Click continue to console.
- [ ] Enable authentication in firebase console by clicking authentication in the menu click Get Started  then select sign-in method tab. Click on email/password and slide the first one over to enable then hit save.




## How to use `.env`

  When connecting to FireBase. We want to use a `.env` file, a place to put environment specific sensitive data. This includes  `user`, `database names`, `API_keys`, and etc. The final step to safeguarding our sensitive information is to include our `.env` file in a `.gitignore` file so our git software will *ignore* the `.env` file and not push it up to the repo when we commit changes.

- [ ] First `cd` into the root directory and `touch .env` will be put there.
- [ ] Create React app will have a `.gitignore` file go to it and type `.env` to ignore the file.
- [ ] Inside the `.env` copy the data from your firebaseConfig create the following to store your sensitive data.

=== ".env"

```yaml
REACT_APP_FIREBASE_KEY="AIzaSyfu8X8rJtQ82YQpYF-SrLg6VKr90uGN5hg"
REACT_APP_FIREBASE_DOMAIN="test-learn-876668g.firebaseapp.com"
REACT_APP_FIREBASE_PROJECT_ID="test-learn-876668g"
REACT_APP_FIREBASE_STORAGE_BUCKET="test-learn-876668g.appspot.com" 
REACT_APP_FIREBASE_SENDER_ID="54980240976"
REACT_APP_FIREBASE_APP_ID="1:667664985586:web:27ce56b3475ad9ffa86P"
REACT_APP_FIREBASE_MEASUREMENT_ID="G-75ed0jhjm9"
```
Use the firebaseConfig credentials you saved earlier to put them in the `.env` with the corospnding name use the above as an example. Make a file in the src directory and `firebase-config.js`. `process.env` is a node variable the stores your `.env` enviroment variables.
=== "src/firebase-config.js"
```javascript
   // src/firebase-config.js
import { initializeApp } from "firebase/app";
import {  getAuth } from 'firebase/auth'

const firebaseConfig = {
  apiKey: process.env.REACT_APP_FIREBASE_KEY,
  authDomain: process.env.REACT_APP_FIREBASE_DOMAIN,
  projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
  storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: process.env.REACT_APP_FIREBASE_SENDER_ID,
  appId: process.env.REACT_APP_FIREBASE_APP_ID,
  measurementId: process.env.REACT_APP_FIREBASE_MEASUREMENT_ID
};
// Initialize Firebase
const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
```

## How to Authenticate with FireBase

Find the App.js file then add code bellow for signing up a user to [authenticate](https://firebase.google.com/docs/auth/web/password-auth) in FireBase. The data is stored on a cloud server based on the credentials in the config file. see the results in the FireBase Dashboard under Authentication. In addition you will see `auth.currentUser` is logged at the bottom.

```javascript
// App.js
import React, { useState, useEffect  } from 'react';
import { auth } from '../firebase-config';//credentials provided by firebase from above
import { createUserWithEmailAndPassword, signOut } from 'firebase/auth' // installed firebase dependency 

function App() {
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
    console.log(error.message);
    }
};
  const logout = async () => {
    await signOut(auth);
  };

console.log("auth.currentUser", auth.currentUser);
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
          <button onClick={logout}> Sign Out </button>
    </div>
);
}
export default App;

    
```
Reminder the info you enter will appear under the Users tab in the Authentication section of FireBase. Also, Look at the documentation and extra resources and play around with the code and FireBase AUthentication console. In the project for class 8 you will implement logging in and proteced routes for FireBase.

## Additional Resources

- [ ] [React Firebase Authentication Tutorial](https://www.youtube.com/watch?v=9bXhf_TELP4)


## Know Your Docs

- [ ] [FireBase Training Docs](https://firebase.google.com/docs/auth)

