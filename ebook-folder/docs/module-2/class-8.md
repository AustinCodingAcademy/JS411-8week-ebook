# Class 8: Protected Routes

<!-- ! HIDE FROM STUDENT; INSTRUCTOR ONLY CONTENT -->
<!-- ## Instructor Only Content - HIDE FROM STUDENTS -->
<!-- cp workspace/resources/classOutlineTemplate.md docs/module- -->
<!-- ! END INSTRUCTOR ONLY CONTENT -->

*It is always the simple that produces the marvelous. —Amelia Barr*

## Greet, Outline, and Objectify

<!-- SMART: Specific, Measurable, Attainable, Relevant, and Timely. -->
<!-- https://examples.yourdictionary.com/well-written-examples-of-learning-objectives.html -->
  
*OBJECTIVE: Today the student will learn and practice to understand:*

* *Using Boolean logic to allow a user access to specific components*
* *Setting cookies in the user's browser*

*****

- [ ] Questions for Student-Led Discussion
- [ ] Interview Challenge
- [ ] Student Presentations
- [ ] Creation Time
    * [ ] Fork and Clone the 411_wk4_day2_protected_routes repo
    * [ ] Follow the instructions in the README to complete then turn in.
- [ ] Push Yourself Further
<!-- - [ ] Interview Questions: Blog to Show You Know -->
- [ ] Exit Recap, Attendance, and Reminders

### Questions for Student-Led Discussion, 15 mins
<!-- This section should be structured with the 5E model: https://lesley.edu/article/empowering-students-the-5e-model-explained -->

[Questions to prompt discussion](./../additionalResources/questionsForDiscussion/qfd-class-8.md)

### Interview Challenge, 15 mins
<!-- The last two E happen here: elaborate and evaluate  -->
<!-- this sections should have a challenge that can be solved with the skills they've learned since their last class. -->
<!-- ! HIDDEN CONTENT: INSTRUCTOR ONLY -->
[See Your Challenge Here](./../additionalResources/interviewChallenges.md)
<!-- ! END HIDDEN CONTENT: INSTRUCTOR ONLY -->

### Student Presentations, 15 mins

[See Student Presentations List](./../additionalResources/studentPresentations.md)

## Creation Time, 60-90 mins

Today we are going to practice what we learned about Protected Routes. We will create a login page, set cookies, and build protected routes to provide a more reliable login experience for the users of the cars application we worked on before.

![fake-car-login-example](./../images/fake-car-login-example.png)

- [ ] Fork and clone the following repository: [411_wk4_day2_protected_routes](https://github.com/AustinCodingAcademy/411_wk4_day2_protected_routes).
- [ ] Follow the directions in the README.md to complete the project.
`git status`, `add`, `commit`, `push` to your forked repo.
- [ ] Turn in the link of your forked repo.

The project directions are also summed up below:

- [ ] We are adding a login page to the FakeCars.com application. Once complete, you will be able to log in to the app and you will remain logged in on page refresh until the cookie expires at one minute's time.
- [ ] You should see a login page when the app first starts. Go ahead and log in. Notice that it takes you to the home page. Now, click the "logout" button. You should have been logged out and taken back to the "/login" route. But are we ever logged in or out? Click on the "Home" and "About" links on the navigation bar. It looks like we can still access everything.
- [ ] In the `Router.js` file we can see a list of all our routes and paths. Write a `ProtectedRoute` function under the appropriate comment.
- [ ] Write a `checkAuth` function under the appropriate comment. Use the `cookie` module to parse the browser cookies and check the `isLogged` cookie. If it has a value, return `true`, otherwise return `false`.
- [ ] Replace all uses of the Route component (inside of Switch) with ProtectedRoute EXCEPT for the "/login" route. We always want to be able to access that so leave it alone.
- [ ] Upon making the change to ProtectedRoute you should notice that you can no longer access any of the links in the navigation bar. They send you back to the login page because there is no cookie available. Let's make sure we set one when we log in.
- [ ] Go to the `Login` component (under `src/Login.js`) and look at the login function. There is a comment to add the cookie. Set the cookie equal to the following value: `loggedIn=true;max-age=60*1000`.
- [ ] Notice you can now log in and access the pages appropriately. We've set an expiration time of one minute on the cookie so go do something else for a minute and then come back to this site. Refresh the page. Were you directed back to the login page?
- [ ] Follow-up Video: [YT, FreeCodeCamp.org - cookies vs sessionStorage](https://youtu.be/AwicscsvGLg)

### Push Yourself Further

- [ ] Read this [insanely cool article](https://www.netlify.com/blog/2017/01/19/setting-cookies-in-react/) on how one developer at Netlify used cookies to solve an on-boarding problem.

## Blogs to Show You Know

[Blog Prompts](./../additionalResources/blogPrompts.md)

## Exit Recap, Attendance, and Reminders, 5 mins

- [ ] Create FakeCar-Login Assignment
- [ ] Create Class 8 Blog Assignment
- [ ] Prepare for next by completing all of your pre-class lessons
- [ ] Complete the feedback survey

<!-- <iframe id="openedx-zollege" src="https://openedx.zollege.com/feedback" style="width: 100%; height: 500px; border: 0">Browser not compatible.</iframe>
<script src="https://openedx.zollege.com/assets/index.js" type="application/javascript"></script> -->


<!-- TODO Create 3 question exit questions -->

<!-- TODO INSERT Student Feedback From -->

<!-- TODO INSERT *HIDDEN* Instructor Feedback Form -->

<!-- 
height/width = 1.777 ---- width="655" height="368"
cp workspace/resources/classOutlineTemplate.md docs/module-
 -->