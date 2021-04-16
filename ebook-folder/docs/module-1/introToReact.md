# Intro to React as a Front-End Library

*Don’t wait for opportunity. Create it. —George Bernard Shaw*

## Recap

At this point in your journey with ACA you should have learned the basic building blocks of web development (HTML/CSS) as well as how to use JavaScript (specifically Node.js) to create your own web server and APIs. Now it's time to learn how to build the front-end of your applications in a professional, dynamic way! It should be noted that you can build front-ends with [multiple libraries or frameworks](https://medium.com/datafire-io/libraries-vs-frameworks-626cdde799a7) including [Angular 8+](https://angular.io/), [Ember](https://emberjs.com/), and [Vue](https://vuejs.org/), but in this course we're going to learn to build with [React](https://reactjs.org/). Learning this library will give you experience with a well-known and popular library, prime you for hiring in the start-up and corporate tech scene, as well as teach you skills to pick up and learn other libraries and frameworks as your career progresses.

## Overview

Let's start with what React is. It's a library. More specifically it's a front-end library just like Vue.js or Angular.js or Backbone.js and so on. It's a library that we can use to speed up the development of our app as well as address performance issues and maintain a composable structure and most importantly, MAKE DEVELOPMENT MORE FUN! We'll break each of these down ahead.

<!-- ! Video Contents: Vimeo, Clayton@ACA - React, the Why - 411.1.1.1 -->
<iframe src="https://player.vimeo.com/video/490887629" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### Read It - What's React?

[React](https://reactjs.org/) was created by Facebook as a solution to a few problems:

1. When something in the DOM changes the entire page must re-render. Go to any site that doesn't use React and you will see that this can take a while, especially if you are viewing the site with a mobile device. Turns out, most people view Facebook with mobile phones. As the internet connectivity in the United States is limited to 3G, 4G and LTE data transmission, Facebook wanted faster page rendering to ensure people continued using their platform. Remember the 2016 presidential election? Facebook was able to get more people tuned into their platform than common media outlets because they had faster page renderings.
  
  * How does it solve the faster rendering? It maintains a virtual DOM. That is to say it keeps a JavaScript object that represents the DOM, then compares what has been changed in the virtual DOM to the actual DOM and only changes pieces of the actual DOM that changed instead of the entire thing!

2. Notice how Facebook has MANY, MANY elements displaying news feeds, images, videos, friends and ads. This becomes hard to maintain for each user. Think about it! Each user's page looks entirely different from the next. How do they do it? With React! They can create reusable components that take in data and can be rendered or not rendered on the page depending on the type of data they take in. This allows for data to be in control of what's rendered and when rather than the browser rendering and simply displaying the data.
  
  * This is where it gets really cool! In Web 101 you learned how to structure a web page with HTML and style it with CSS. You learned how to manipulate data in JS211 and learned common programming patterns. With React you will be able to use those HTML elements inside the JavaScript you write while injecting CSS to style it . . . ALL IN THE SAME FILE, while also programming what is rendered and when. This, you see, is called **JSX**.

  * Now we get to **composable structure**. Composable structure in our code allows us to build multiple pieces of our app in separate files and then call them, like functions, in the main part of our app if/when we need them! If you haven't picked up already, functions are just recipes that are built and laid out ready to be used. They are not used until they are called. In React, we can lay out functions that return HTML, CSS and JS to be used if/when we need them.

3. Lastly, React is really fun to build with! No longer are you stuck using all the DOM methods like `.getElementById()` and `.innerHTML()`. React itself uses these under-the-hood, you use one of them and from then on you don't have to think about the DOM methods. Simply write JavaScript and render what you want, when you want and how you want!

### How Does React Work?

There are a couple of pieces we'll cover first then you can start putting it all together for yourself.

####  Functional Components

**Functional Component** are just that, **components** that can be called as normal JavaScript functions. Let's say you had a page like YouTube and all the videos that showed up in your search results for "hamsters on piano" included videos you have already seen. If you wanted to display to the user their previously watched videos with a banner that says, *"you watched this on dd/mm/yyyy"* you could do that with a functional component. You would build the functional component to show the video and title that shows up in the search results. Then the component could query your history and if it matches any of your history it could use an if/else statement to display the banner if you had watched it or not if you haven't watched it.

Let's look at a simpler example for right now. In the component below we're going to build a button in a functional component that will display either "Was button clicked? true" or "Was button clicked? false" based on whether the button was clicked or not. We'll call this component in a parent component that will hold the state of the button, `isClicked: false`. We'll then pass the state of the button back to the child component, `MyFirstComponent.js` via props.

Check it out.

=== "MyFirstComponent.js"

    ```javascript
      // because React is a library we have to call the functionality of it we want to use.
      // To do this we will always have to write the following line at the top of our .js file to save the functionality to a variable
      import React from 'react';

      // simply write a function in ES6+ then pass in the keyword props to access this special object
      const myFirstComponent = (props) => {
        // every component in React MUST return something...
        return (
          <button>
            Was button clicked? {props.wasClicked}
          </button>
        )
      }

      // Then, because we want to compose our web pages with composable elements, we have to export the code in the file. Always write this line at the end of your .js files:
      export default myFirstComponent
    ```

=== "Without Comments"

    ```javascript
      // MyFirstComponent.js
      import React from 'react';

      const myFirstComponent = (props) => {
        return (
          <button>
            Was button clicked? {props.wasClicked}
          </button>
        )
      }

      export default myFirstComponent
    ```

#### Class-Based Components pt.1

Now let's see what a **class-based component** looks like. Because we need to hold the state of our button and create a method to take the input of the `onClick` of the button, we'll need to make our parent component of this button a class-based component. This is important. Most components you build will be functional, but as you learn that it needs to hold state or have methods, you'll then change them over to be these class-based components. Check it out . . .

=== "MyFirstClassComponent.js"

    ```javascript
      // Again import React to use it but this time we have to destructure it and get to the "Component" key
      import React, {Component} from 'react'
      // We can also import code we've already built into these class-based components
      import myFirstComponent from './MyFirstComponent'

      // Notice here we use that "extends" word on the "Component" we imported?
      class MyFirstClassComponent extends Component {
        // All Classes must have a "constructor", in React we always pass "props"
        constructor(props) {
          // Remember that if we "extend" a "class" of a "class" we have to call the "super()" method. Just pass it "props" as well.
          super(props);
          // Class-based Components allow us to have "state"! And this is why/when we use class-based components.
          this.state = {
            text: '',
            todos: [],
            isClicked: false
          };

          // Class-based components also allow us to have methods attached to them
          onChange = e => {
            this.setState({
              text: e.target.value
            })
          }

          // Class-based components must have the "render()" method in them for React to call them as an IIFE (immediately invoked function expression)
          render() {
            // and the "render()" method must have a return
            return (
              <div>
                <h1>Input Text Below</h1>
                <input value={this.state.text} onChange={this.onChange}/>
                {/* We can make comment in JSX like this, with curlies outside our comment tokens*/}
                {/* We can invoke myFirstComponent here to use it in this component and pass it information via "props"*/}
                <myFirstComponent wasClicked={this.state.isClicked} />
              </div>
            )
          }
        }

      export default MyFirstClassComponent
    ```

=== "without Comments"

    ```javascript
      // MyFirstClassComponent.js

      import React, {Component} from 'react';
      import myFirstComponent from './MyFirstComponent'

      class MyFirstClassComponent extends Component {
        constructor(props) {
          super(props);
          this.state = {
            text: '',
            todos: [],
            isClicked: false
          };

          onChange = e => {
            this.setState({
              text: e.target.value
            })
          }

          render() {
            return (
              <div>
                <h1>Input Text Below</h1>
                <input value={this.state.text} onChange={this.onChange}/>
                <myFirstComponent wasClicked={this.state.isClicked} />
              </div>
            )
          }
        }

      export default MyFirstClassComponent
    ```

You can see that our button element, `myFirstComponent`, is called in our parent component's `render()` method and we pass it the prop: `wasClicked` which is pointing at the parent component's state object, `isClicked`. Then if you scroll back up and look at the `myFirstComponent` code you'll see we can display the state by placing the `props.wasClicked` inside curly braces `{}`: `{props.wasClicked}`. Take some time to make sure you have some general grasp of the way these are threaded together.

  > Pretty simple right? Cool!

### BIG NOTES you MUST remember:

- [ ] Each component **can & must only return ONE** parent element. Which means if you want an `<h1/>`, `<p/>` and a `<button/>` element to be returned from a component it must be wrapped in a parent element like a `<div/>` or `<article/>`. This is a hard and fast rule you must follow when developing with React.

- [ ] **Class-based components** must start with a capital letter!!!! You know this from JS211 about classes. It still applies here. Don't forget it or you'll be chasing the same bug every day.

- [ ] Title your file names the same as your components. This is the standard way of doing it.

- [ ] You don't have to include `.js` in your import statements as long as it is a `.js` file. If it's anything else, `.ts`, `.css`, `.html`, or anything else, you still have to put the file type. But JavaScript files don't have to be declared, React makes *js* assumptions for you.

- [ ] Though we'll be starting with **Class-Based components** as a way to get us into the mindset of developing with React it's important to know that **Functional Components** using **Hooks** to manage component state has become the norm and preferred technique circa 2019-2020+. Most apps have one and only one class based component.

## Know Your Docs

- [ ] [NPM Docs - npx](https://www.npmjs.com/package/npx)
- [ ] [React Docs - Home Page](https://reactjs.org/)


<!-- ! END OF VIDEO 101.1.3.1 - TITLE-->
<!-- ? Video Numbering and Title system: CourseNumber.ModuleNumber.LessonNumber.VideoNumber -->
<!-- * (VIDEO 101.2.4.3 - "CSS Selectors") === 101 Course, Module 2, Lesson 4, Video 3 - "CSS Selectors" -->

<!-- 

cp workspace/resources/templateFile.md docs/module- 

```javascript

```

| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | Fetch resource                       |
| `PUT`       | Update resource |
| `DELETE`    | Delete resource |


    `line numbers`
:do you like 'em?


++slash++
https://facelessuser.github.io/pymdown-extensions/extensions/keys/

=== "Javascript"

    ```javascript
    ```

=== "Python"

  ```python
  ```

=== "Example"
    ```console
      .
    ```

=== "Instructions"
    ```markdown
      .
    ```

=== "Result"
    ![PIC](./../images/pic.png)
-->