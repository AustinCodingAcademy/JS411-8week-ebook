# App Deployment

*Happiness is a butterfly, which when pursued, is always just beyond your grasp, but which, if you will sit down quietly, may alight upon you. —Nathaniel Hawthorne*

## Overview

We learned in the last class why deploying our apps is a necessity. *We want everyone on the internet to be able to access what we've created, right?* Now we'll deploy our Fake Cars App we have spent so much time working on. Then eventually you can use these directions and what you learn here to deploy your Capstone app and everything else you build in the future!

### Pre-Deployment and Preparation

- [ ] If you have the functions emulator line of code, (whether you are going to use functions or not) comment out the emulator code.

![firebase-deploy-commentOutFunctionsEmulator](./../images/firebase-deploy-commentOutFunctionsEmulator.png)

- [ ] You should have Firebase tools installed already from the directions in the [serverless function](./../module-3/serverless.md) lesson. If not run `npm install -g firebase-tools`.
- [ ] Same with Login to firebase CLI. Run `firebase login` to see if you are logged-in. If not, do so with the same email/account as used for your firebase account.

## Deploying with FireBase

We are going to deploy our [Fake Cars assignment we started in Class 8](../module-2/class-8.md). You can use these directions to deploy any React project including your Capstone App for graduation. 

> NOTE: If you're unable to see them clearly zoom-in on the picture with ++ctrl++ + ++plus++ .

- [ ] Make sure you're in the root directory of your project.

- [ ] Run `npm run build`

![deploy-firebase-runBuild](./../images/deploy-firebase-runBuild.png)

- [ ] initialize the project `firebase init`

![firebase-init-deploy](./../images/firebase-init-deploy.png)

- [ ] Are you ready to proceed? Type ++y++ 

- [ ] Select Hosting: Configure files for Firebase Hosting and *optionally* set up GitHub Action deploys. Use arrow keys to move and  ++space++ to make selection then press ++enter++ to confirm selection and to continue.

![firebase-deploy-selectingHostingOptions](./../images/firebase-deploy-selectingHostingOptions.png)

- [ ] Select "use an existing project"

![firebase-deploy-selectExistingProject](./../images/firebase-deploy-selectExistingProject.png)

- [ ] Then select your project by name, Fake Cars...etc.

- [ ] What do you want to use as your public directory? (public) type  `build`

![firebase-deploy-buildPublicFolder](./../images/firebase-deploy-buildPublicFolder.png)

- [ ] Configure as a single-page app (rewrite all URLs to /index.html)? Press ++y++

- [ ] Set up automatic builds and deploys with GitHub? Press ++n++

- [ ] File build/index.html already exists. Overwrite? Press ++n++

- [ ] Run `firebase deploy --only hosting`

![firebase-deploy-selectHostingOnly](./../images/firebase-deploy-selectHostingOnly.png)

You will get a URL with the link to your deployed site in the terminal and can also be found on your FireBase console under "Build" >> "Hosting".

![firebase-deploy-urlDomainLink](./../images/firebase-deploy-urlDomainLink.png)

### Serverless Cloud Functions Deploy

If your app is using serverless cloud functions use the following directions. **You will have to upgrade to a paid plan.** This is very common with cloud deploys involving back-end server side code. Remember there is a free tier with no charge if your app stays under a certain amount of data usage and you can set a budget later. Reference the [pricing guide](https://firebase.google.com/pricing) for more details.

 - [ ] Click "Upgrade project" under the functions menu and follow the directions and prompts with your relevant information.

 ![firebase-deploy-upgradeProjectForFunctions](./../images/firebase-deploy-upgradeProjectForFunctions.png)

 - [ ] Set your budget.

 ![firebase-deploy-setBudget](./../images/firebase-deploy-setBudget.png)

- [ ] In your terminal run `firebase deploy --only functions`. If you get errors follow directions below; otherwise, go test your app and see if your live deployed app works as expected.

#### Errors

- [ ] If you get the **CLRF LF error**: click on `.eslintrc.js` and comment out the entire file. Eslint is just for formatting and code styling; it will not change how your app works. Also, this `.eslintrc.js` file only works for our `functions/index` file. The eslint used for all our React/front-end code will not be affected. There is a potential bug with line formatting and the version of eslint used in functions folder, so this will help us get our app deployed. 

![firebase-deploy-commentOutEslint](./../images/firebase-deploy-commentOutEslint.png)

#### Re-Run Deploy

When you've built a new version of your app and you just need to update the deployed version, without having to go through all the previous steps again, just run these:

- [ ] Run `npm build`
- [ ] Run  `firebase deploy --only hosting`
- [ ] And or run `firebase deploy --only functions` for cloud functions changes. 

## Additional Resources

We normally provided you with a link to the official documentation of any subject we teach in the pre-homework, but today we'll leave with you with a number of resources that may help you build your Capstone Project or other apps in your future.

- [ ] **[Migrate to AWS, a Cheaper Deployment Strategy for Students](https://www.notion.so/Connect-MySQL-workbench-to-AWS-RDS-Free-tier-a95068f5d6b84383ac0af2fd7bfe15f6)** - GCP is usually cheaper to get started with but you may soon lose credits. As an alternative one of our instructors, Matt Huntsberry, as put together a tutorial to help you host with AWS when your GCP credits run out.
- [ ] [Typography](https://femmebot.github.io/google-type/) - Seriously, if you have no eye for design but care that your app is beautiful you may want to use this site for some ideas and code.
- [ ] [Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/) - When designing your app I hope you came across this website but if not here it is. A full idea of designing an application, atomically!
- [ ] [Front-End Design Checklist](https://codeburst.io/the-front-end-design-checklist-4dd15828fad) - Maybe you came across this too in your google-ing. Nonetheless, it is a rad resource for any developer of any experience.
- [ ] [API First Development](https://konghq.com/blog/three-ways-api-first-development-is-the-future-of-web) - Think your backend is less important? Think again.
- [ ] [Building with Angular Material Tutorial](https://auth0.com/blog/creating-beautiful-apps-with-angular-material/) - a clean crisp guide to Angular intricacies.
- [ ] [Front-End Designs](https://www.toptal.com/front-end/front-end-design-principles) - If you care about design and want to know more...
- [ ] [Google.io](https://auth0.com/blog/creating-beautiful-apps-with-angular-material/) - Shadow DOM, HTML Templates - Want to know more about the DOM and Shadow DOM? Ask google.
- [Planning a Front-End JavaScript Application](https://www.telerik.com/blogs/planning-front-end-javascript-application) - JavaScript is awesome and older developers are stupid. Make sure you get the real scoop on what JS can do and how you should approach it.
- [ ] [Human JavaScript](http://read.humanjavascript.com/ch00-foreword.html) - For your time after graduation when you're looking to get stronger in your skills. Get to reading this book!
- [ ] [Dispelling Bullshit](http://pragmatic-backbone.com/overview-and-bullshit-dispelling) - Angular, React, Backbone, Ember, Vue, it doesn't matter. Build and learn how to build well and you will do well!
