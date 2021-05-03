# CRA (create-react-app) + ToDo App Walk-through

## Overview

For the rest of this class, we'll be using the create-react-app tool to well...create react apps.

This lesson will be comprised of a series of videos building upon each other to walk you through using CRA and to build your first project. It's important to follow along in your text editor, understand what's going on in each and make sure you see each of them through completion.

### [Starting with React video](https://vimeo.com/491807004/da1cc42c99)

- [ ] See what [npx](https://www.npmjs.com/package/npx) is.
- [ ] How to create a React app.
- [ ] Where the entry-point of all React apps is.
- [ ] How to navigate the first 3 files of a React app.
- [ ] And the first rule of building with React: Component can only return one parent element.

<!-- ! Video Contents: Vimeo, Clayton@ACA - Starting with React - 411.1.1.2 -->
<iframe src="https://player.vimeo.com/video/491807004" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### Create-React-App

- [ ] See what is installed in the **npx create-react-app** command.
- [ ] How to run a React App.
- [ ] Make your first change.
- [ ] Follow the flow from the app's entry-point(`index.html`) to what you see on the screen.
- [ ] Learn how to initialize a folder as a git repository and push it from local to remote.

<!-- ! Video Contents: Vimeo, Clayton@ACA - Create React App Overview - 411.1.1.3 -->
<iframe src="https://player.vimeo.com/video/491812908" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### Convert Functional Component to Class-based Component

- [ ] Learn what component state means
- [ ] How to convert a Functional Component to a Class-Based Component
- [ ] import Component
- [ ] exchange function keyword for class keyword
- [ ] build constructor and call super
- [ ] build state object
- [ ] and build a render method.

<!-- ! Video Contents: Vimeo, Clayton@ACA - Functional to Class Component - 411.1.1.4 -->
<iframe src="https://player.vimeo.com/video/491818181" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### JSX & Add Button + State Change

- [ ] Use JSX to render pure JavaScript within your HTML.
- [ ] Build a button.
- [ ] Build a method to be called when the button is clicked.
- [ ] Update state in the method.
- [ ] And render the state change on the screen.

<!-- ! Video Contents: Vimeo, Clayton@ACA - JSX to Add a Button and Change State onClick - 411.1.1.5 -->
<iframe src="https://player.vimeo.com/video/491828632" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### Add Input

- [ ] Create a **visual** cue for the human-user to input data into.
- [ ] Create a new property on the state so you can **store** the data from the human user.
- [ ] Create a method that **moves** the data from the input field to the state & is called with the onChange event listener.
- [ ] Repeat the "Three Jobs of a Developer" again for the form submit:
  
    * [ ] Add submit button and call another method when clicked
    * [ ] Create a place for the data to be stored in the state.
    * [ ] Create a method to move the data from the "input value" property to "listOfTodos" property and clear the "inputValue".

<!-- ! Video Contents: Vimeo, Clayton@ACA -  Add Input Field, Store Value in State, and Render - 411.1.1.6 -->
<iframe src="https://player.vimeo.com/video/491833816" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### `.map()` Todos

- [ ] use `.map()` function to display all items in the `this.state.listOfTodos` array
- [ ] use the index to create a "unique" `key=` each child element

<!-- ! Video Contents: Vimeo, Clayton@ACA - .map() Over the Todos - 411.1.1.7 -->
<iframe src="https://player.vimeo.com/video/491840476" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Know Your Docs

- [ ] [React Docs - create-react-app](https://reactjs.org/docs/create-a-new-react-app.html)
- [ ] [NPM Docs - npx](https://www.npmjs.com/package/npx)
