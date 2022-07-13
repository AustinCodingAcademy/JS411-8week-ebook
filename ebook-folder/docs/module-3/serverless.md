# Intro To Serverless


**Serverless** refers to functions that run on the back end to help developers build and run applications without having to manage servers. They are no different from the functions you have written in the past.

 There are still servers in ***serverless***, but you do not have set them up or manage them. A cloud provider handles the routine work of provisioning, maintaining, and scaling the server infrastructure. Simply write your code in a designated folder provided by firebase.

 You can think of the ***serverless functions*** as setting up your own api like you have called in the past using fetch. However, instead of using fetch to communicate with the backend you use firebases built in methods. You will be writing ***serverless functions*** in ***node.js*** so it is considered part of the backend along with your database.


#### Why Serverless?
- [ ] **Security**: Every thing is exposed on the front end client. Having a backend to do sensitive operations is very important.
- [ ] **Versatility**: You can have your backend do something independent of the front end.
- [ ] **Low code setup**: Firebase does all the infrastructure and server side code for you. The only thing you need to focus on is the task you are trying to accomplish with your code.
- [ ] **Api usage**: Some api's require backend code like **node.js** to utilize them.



## Set up Serverless 

We will walk through the steps to use your first **serverless function**. FireBase refers to their serverless functions as [cloud functions](https://firebase.google.com/docs/functions).



1. Open and `cd` into the root directory of the [learn-firebase](../module-2/implement-fireBase.md) project you have been learning with. `cd learn-firebase`

2. In the root directory of [learn-firebase](../module-2/implement-fireBase.md) run `firebase init functions`.



    ![firebase-createApp-3Create](../images/firebase-init-functions.png)

3. Initialize in this directory `Are you ready to proceed? (Y/n)` type `y`. 

4. Next Press enter and select `> Use an existing project`.

5. Use the arrow keys to select your project name from FireBase.

6. The language to write Cloud Functions select `javaScript`.

7. Use ESLint to catch probable bugs and enforce style. Type `y`

8. Install dependencies with npm now. Type `y`

9. You should see A functions folder and if you look inside it notice that it has a separate `package.json` and `node_modules` and an `index.js`.

10. Our first FireBase function. look in `functions/index.js`. This is where we will write our functions. You will see a commented out function. We are going to run this function so uncomment it.

11. First `cd` into the `functions` directory. Then type `firebase emulators:start`

12. You should see a message in the terminal like this `functions[us-central1-helloWorld]: http function initialized (http://localhost:5001/learn-firebase-57df8/us-central1/helloWorld).` with your project name in the middle after the port number.

    ![firebase-createApp-3Create](../images/first-serverless-function.png)

13. Press control and click it in your terminal or copy and paste it into your browser. What do you see? what happen?



## Cloud Functions
We now have the power of an entire backend and server infrastructure  just by writing functions. In future lessons we will use This backend with our front end code and do operations and tasks that require the security of a backend environment.

## Additional Resources



- [ ] [How do Cloud Functions work?](https://www.youtube.com/watch?v=rERRuBjxJ80)


## Know Your Docs

- [ ] [Cloud Functions](https://firebase.google.com/docs/functions)


