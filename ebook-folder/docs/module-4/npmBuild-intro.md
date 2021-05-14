# NPM Build

*Don’t stop when you’re tired. Stop when you’re done.*

## Review and Recap

Hopefully all of this planning is bringing to you clarity of your app and the work ahead. I'm sure you've never thought like this and it's opening new pathways in your mind. This is a good thing! Learning to program and learning to program well are two different skills that will help you do other things in your life better.

If you didn't believe it before, believe it now: there's still more planning to your app before you actually get to build. Crazy, right!? This is what actually goes into the apps you know and love. For every app you use there is a paper mockup of it. There is a flow chart, code plan, and kanban board used to build it.

Today we're going to continue with npm and planning the User Flow of our app. In class we'll be planning our Capstone Project and working on our ATX-Small Business App!

## Overview

Why are we talking about the `npm build` command? This is something you should already know about and have hopefully been using throughout this course. The purpose of this pre-work isn't to re-introduce you to the command, it's to explain what's going on behind the scenes when you run it.

## Why `npm build`

To understand what's happening we first need to remind (or inform) you that the browser can't naturally read React code. What do I mean when I say the browser? Chrome. Firefox. Edge. And why does it matter what the browser can read? Well because that's where our applications are running. They are websites, after all!

You may have already known all that but it's important to reiterate. Now, because the browser can't naturally read code that looks like this:

=== "Simple React Component"

    ```javascript
    export MyComponent = (props) => (
      <div>
          <h1>Welcome to my component</h1>
      </div>
    )
    ```

...because it's neither plain JavaScript nor HTML (it's a mixture of both), we need to do something with this code to format it in a way that the browser can read. There are two main things we need to do.

1. **Transpilation**

We need to transpile our code into something the browser knows how to read. We need to transpile it into plain JavaScript. Additionally, you may be writing code in new ES ways that aren't supported in the browser yet. For example, for a while ES6 functionality like arrow functions and imports wasn't supported in the browser (it is now) so we needed to transpile that code in ES2015 format.

2. **Minification**

We need to make the files as small as possible. That means removing all extra space in our files and sometimes changing variable names from something longer like `myFunction` to `mf` (hehe). Why are we doing this? Because it decreases the time it takes for the browser to load the file. The smaller the file, the better the performance on the web.

Don't worry, `create-react-app` handles all this logic behind the scenes and you don't need to do anything extra. Just know that transpilation and minification are some of the main things that are happening when you run the `npm build` command. Let's look at some examples.

### The Build Folder

When you run the `npm build` command a folder is generated called `build`. Let's look at what's inside:

=== "Build Folder Structure"

    ```console
    -- static
    -- asset-manifest.json
    -- favicon.ico
    -- index.html
    -- logo192.png
    -- logo512.png
    -- manifest.json
    -- precache-manifest...
    -- robots.txt
    -- service-worker.js
    ```

You'll notice that a lot of this is basically copied over from the "public" folder we talked about last class. We want to focus on the two main parts of this build folder: `index.html` and the `static` (folder).

`index.html`
This is the main starting point of your application. To see what's changed since the `public/` folder, let's open up the `index.html` file from the `build/` folder. You may notice that it's all on one line. That's because it's been **minified**. Well it's super ugly and we actually want to look at certain parts of it so go ahead and navigate to the following website: [https://unminify.com/](https://unminify.com/). Once there, copy the contents of `build/index.html` and paste them in the box. It should have formatted the content for you.

Near the top of this file you should see the following: `<link href="/asset-v1:ACA+JS411+09282020_JS411_C6+type@asset+block/css_main.34de6062.chunk.css" rel="stylesheet">` That's all the bundled css that exists in your application, all in one file.

Near the bottom of the file you should see the following: `<script src="/asset-v1:ACA+JS411+09282020_JS411_C6+type@asset+block/js_2.c633e371.chunk.js"></script>` That's all the bundled javascript code (all of your React code) in one file.

> NOTE: The random numbers get generated different when the build is run so don't worry if your filename isn't exactly the same.

`static`
If you notice above, both the css link and the javascript `script` reference `/static/`. That represents the static folder in your "build" folder. That's where all the transpiled and minified code lives. It's all the code you've written in React, just in a different format. Let's go take a look at these files.

Go to the `static/js` folder and click on the top file. Don't worry about the other ones in this folder. The file we are looking for should end in `chunk.js`. The file should look similar to this:

=== "Minified Code"

    ```javascript
    (window["webpackJsonpmy-ssr-app"]=window["webpackJsonpmy-ssr-app"]||[]).push([[
      2],[function(e,t,n){"use strict";e.exports=n(4)},function(e,t,n){"use strict";
      var r=Object.getOwnPropertySymbols,l=Object.prototype.hasOwnProperty,i=Object.
      prototype.propertyIsEnumerable;function a(e){if(null===e||void 0===e)throw new
       TypeError("Object.assign cannot be called with null or undefined");return Object
       (e)}e.exports=function(){try{if(!Object.assign)return!1;var e=new String("abc")
       ;if(e[5]="de","5"===Object.getOwnPropertyNames(e)[0])return!1;for(var t={},n=0;
       n<10;n++)t["_"+String.fromCharCode(n)]=n;if("0123456789"!==Object.getOwnPropertyNames
       (t).map(function(e){return t[e]}).join(""))return!1;var r={};return
       "abcdefghijklmnopqrst".split("").forEach(function(e){r[e]=e}),"abcdefghijklmnopqrst"
       ===Object.keys(Object.assign({},r)).join("")}catch(l){return!1}}()?Object.assign:
       function(e,t){for(var n,o,u=a(e),c=1;c<arguments.length;c++){for(var s in n=Object
       (arguments[c]))l.call(n,s)&&(u[s]=n[s]);if(r){o=r(n);for(var f=0;f<o.length;f++)i.
       call(n,o[f])&&(u[o[f]]=n[o[f]])}}return u}},function(e,t,n){"use strict";!function 
       e(){if("undefined"!==typeof __REACT_DEVTOOLS_GLOBAL_HOOK__&&"function"===typeof 
       __REACT_DEVTOOLS_GLOBAL_HOOK__.checkDCE)
    // ...etc...
    ```

=== "Zen"

    <div style="width:100%;height:0;padding-bottom:66%;position:relative;"><iframe src="https://giphy.com/embed/H7kfFDvD9HSYGRbvid" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div>

### Summary

This seems like a lot of information but you really don't need to know all of it in detail. What you need to understand is that the `npm build` command gets your code ready for a production environment by bundling it (**transpiling** and **minifying**) into a `build/` folder that contains static files.

What this also means is that you don't have to run `npm start` anymore (after you've built). We'll explore that in the practice section and show you how your app would run in production.

## Practice It

<!-- https://studio.zollege.com/container/block-v1:ACA+JS411+09282020_JS411_C6+type@vertical+block@d028f2de03aa43dbaaf94a1df49308bf -->

We are going to create a new project with create-react-app, build the app and then load the static files from our browser.

- [ ] Run `create-react-app build-ex` to create a project called `build-ex`
- [ ] Navigate to that folder and run `npm i` to get all your dependencies
- [ ] Now run `npm start` to see the default create-react-app which you should have seen a couple times by now
- [ ] Run the `npm build` command. It should have generated the `build/` folder that we've been talking about today. Since we've already explored the contents of that file, we don't need to do that again here
- [ ] Now, in VSCode (or another editor) right-click on the build folder and select "copy path"
- [ ] Open a new web browser tab and paste the file path into the browser. You should see a directory show up. Click on the `index.html` file. That's the main starting point of your application
- [ ] Don't see anything? Add `"homepage": "."` as a property to the bottom of your `package.json` object and re-run `npm build`. This will sync all the files to the current folder. Now reload the page and you should see your app loaded

> Note: If you could not copy the exact path you can type file:/// in the browser and navigate to that build folder manually.

## Additional Resources

- [ ] [YT, Hitesh Choudhary - How to Deploy A React App](https://www.youtube.com/watch?v=ZKxvBsGVKR8)
- [ ] [Tool, Unminify](https://unminify.com/)

## Know Your Docs

- [ ] [NPM Docs - Home](https://docs.npmjs.com/)
