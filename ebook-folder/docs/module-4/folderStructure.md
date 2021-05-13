# Folder Structure + App Planning Pt.2

*The key to success is to focus on goals, not obstacles.*

## Review & Recap

Heads up! This week is another App development week where you will have the entirety of the time to build a working application based on the specifications provided on the class page.

That being said, we think it's useful to keep providing you with content in these pre-work sections. It will help you gain more understanding and hopefully inform you on topics that might come up in your interview questions when you are applying for developer jobs, so don't skip this.

## Overview

We're going over this because we think it's important that you understand the "why" behind what we are doing. You've seen .gitignore and other various files but you might not fully understand why we would want to "ignore" these files for example. We'll dive into that, and other various topics in a second.

### Folder Structure

When you first run `create-react-app`(CRA) you end up with a directory that looks like this:

=== "Basic CRA Folder Structure"

    ```console
        // my-app
            -- node_modules
            -- public
            -- src
            -- .gitignore
            -- package-lock.json
            -- package.json
            -- README.md
    ```

Let's talk about each of these in some quick detail.

#### `node_modules/`

This folder holds all of your project's dependencies. It is not there by default when you clone something from Git. It gets generated when you run the `npm install` command. If you ran npm install express then you should expect to see a folder titled `express` underneath `node_modules`. Since React is installed by default with `create-react-app`, we see something like this:

=== "Node Modules Structure"

    ```console
        ...
        -- react
        -- react-app-polyfill
        -- react-dev-utils
        -- react-dom
        ...
    ```

What are `react-app-polyfill `and `react-dev-utils`? I didn't install those? You're right, that means something else probably did. If you expand one of those folders underneath `node_modules` you'll see that they each have their own `package.json` file just like our project does. ...Our dependencies also have dependencies...inception.

=== "Inception 1"

    <div style="width:100%;height:0;padding-bottom:69%;position:relative;"><iframe src="https://giphy.com/embed/7pHTiZYbAoq40" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div>

=== "Inception 2"

    <div style="width:100%;height:0;padding-bottom:71%;position:relative;"><iframe src="https://giphy.com/embed/kOIbusN7fPnkk" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div>

=== "Inception 3"

    <div style="width:100%;height:0;padding-bottom:65%;position:relative;"><iframe src="https://giphy.com/embed/1412QM7NaCZMyc" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div>

=== "No GIF"

*****

#### `public/`

The `public/` folder is the main starting point of our app. It holds a few key files for getting started and it's directory structure looks like this:

=== "`public/` Folder Structure"

        ```console
            -- favicon.ico -> image in the corner of browser tab
            -- index.html -> main starting file
            -- logo192.png -> logo image
            -- logo512.png -> different sized logo image
            -- manifest.json -> site settings
            -- robots.txt -> seo settings
        ```

I've briefly pointed out what most of these files do but I want to talk a little more about the main file which is index.html. Everything you put here will be loaded into your app once a "build" is created. If you wanted to use Bootstrap for example you might load in some extra css/js with a `<link>` or `<script>` tag. You would put those in this index.html file. Also of importance . . . look near the bottom of this file in the "body" tags. Notice this: `<div id="root"></div>`. Now go to `index.js` under the `scr` folder and notice this: `ReactDOM.render(<App />, document.getElementById('root'));`. See a correlation? That tag in the `index.html`file is where your whole React app gets inserted/rendered.

*****

#### src

This is the main folder for writing your React code. Its directory structure looks like this:

=== "`src/` Folder Structure"

    ```console
    -- App.css
    -- App.js
    -- App.test.js
    -- index.css
    -- index.js
    -- logo.svg
    -- serviceWorker.js
    ```

Here we have the JS and CSS for the App component, the JS and CSS for the `index.js` file, a `test.js` file, a `logo.svg` and a service worker. Typically, when we start with a React app, we start writing our code in the `App` component. We also typically create a folder called `components/` to hold our custom components and a folder called `containers/` if we hook Redux to our app. Do not worry about the `serviceWorker.js` file. That's an [advanced subject that we won't cover in this course](https://stackoverflow.com/questions/49314386/what-is-service-worker-in-react-js) and it's not required to build React applications.

*****

#### `.gitignore`

This is a file that tells us which files/folders we want Git to ignore. Sounds self-explanatory doesn't it? This means that if we add a file or folder that exists in the `.gitignore` file, Git won't even show it as an untracked file. That means it will never get uploaded to our repository. What kinds of things would we want to be ignored from our repository? `node_modules`, `.env`...?

##### Why Ignore `node_modules/`

Our `node_modules`/ folder is typically very large. Because of that, it takes longer to upload/download from our repository. But there's another reason we don't want these files to be tracked in Git and that's because Git is used for version control. It's used to save a running history of the files we've touched and the changes we've made. We are never going to manually change our `node_modules`.

Let's take it one step further. We already have a blueprint of our `node_modules/` folder locally. That's what our `package.json` file is for. It knows about all the dependencies we need. And we already mentioned that the `node_modules/` folder gets created when we run `npm install`. So there is absolutely no reason to upload our `node_modules/` folder to Github. That rule follows in other languages as well and is considered general best practice. You don't upload your dependencies (any third-party code) to Github.

##### Why Ignore `.env`

Simple put, the `.env` file is ALWAYS filled with **sensitive** information like our API Keys and Database login credentials. For this reason we **NEVER** want to include it with our code pushes to a repo...even if it's a private repo. Instead you can use [GitHub sensitive data tool](https://medium.com/@GeorgiosGoniotakis/how-to-keep-your-repositorys-sensitive-data-secure-using-git-secret-c1ddc28cb985) or add the needed environment variables to the hosting platform manually when you setup your pipeline initially.

> Talk to your instructor to make sure you understand this.

*****

#### `package.json`

As we mentioned above, the `package.json` file keeps a list of all the dependencies you have for your application. But it can do more that that. It's also the place where the "scripts" for your application are stored. These scripts are the commands like `npm start`. For example, by default `create-react-app` provides the following scripts:

=== "`package.json` file"

        ```json
        "scripts": {
            "start": "react-scripts start",
            "build": "react-scripts build",
            "test": "react-scripts test",
            "eject": "react-scripts eject"
        }
        ```

The `start` script runs your application, as you know. The `build` script builds a production version of your application to be served statically (by an express app perhaps). When that script is run a `build/` folder is created on the top level of your application above the `public/` folder. We can talk more about what is actually going on in that process in the next pre-homework and in class. Needless to say, the `package.json` file is basically the **blueprint** of your application. The app won't work without it.

*****

#### `package-lock.json`

This file is an extension of the `package.json` file. It controls the versions for all the dependencies of your dependencies as we saw earlier with the `node_modules/` folder by *locking* them in-place. Before NPM 5, there was only a `package.json` file. That was fine for a long time but eventually developers realized their code was getting out of sync because the sub-dependencies would change versions. Let's give an example.

You run this command `npm i express` and it populates your `package.json` with the following:

=== "Example `package.json` File"

        ```json
        "dependencies": { "express": "^4.17.1" }
        ```

Great. Now everyone that uses your application and runs `npm install` will get express version 4.17.1 and all is good. We realized we had a little problem though and that's because express also has dependencies and so a portion of their dependency tree looks like this:

=== "Example `package.json` File - Varying Dependencies"

```json
    "dependencies": {
        "body-parser": "1.19.0",
    }
```

So what ended up happening is someone would bump the version for `body-parser` to `1.20.0` and `express` would inherit that change without changing its own version and then the code would break because while everyone you shared your app with is still getting express version `4.17.1`, express behind the scenes is now using `body-parser` version `1.20.0` and it's possible that change caused some unexpected side-effect.

Ok . . . that's a lot of information but now that we understand that we can understand what `package-lock.json` does. It essentially **locks** down the whole dependency tree so that every dependency you install, and all of its dependencies will always have the same versions and you won't run into the issues I described above. It's important to commit your `package-lock.json` file to GitHub for this reason.

*****

#### `README.md`

The last file we want to talk about is the `README.md file`. This one is probably the most self-explanatory. Its purpose is to provide instructions/guidelines for setting up and running your application. It should give your users a clue as to what your application does and how to start it. Optionally, you can provide instructions on how to contribute to your project.

### Summary

Hopefully you found this helpful and have a better understanding of what happens when you run create-react-app. In the next pre-homework we'll get into what happens when you build your application.

## See It - CRA and It's Initial Files

<!-- ! Video Contents: YT, LevelUpTUTS - CRA and It's Initial Files-->
<iframe width="655" height="368" src="https://www.youtube.com/embed/rUdtgnwrA14" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Additional Resources

- [ ] [YT, LevelUpTUTS - CRA and It's Initial Files](https://youtu.be/rUdtgnwrA14)
