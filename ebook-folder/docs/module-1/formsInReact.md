# Forms in React

*Keep your face always toward the sunshine—and shadows will fall behind you. —Walt Whitman*

## Overview

We've seen a lot in the past few classes. It may seem like a flurry of information but the more you practice this stuff the easier it will get. Always keep looking up React documentation and tutorials to guide you along. Today let's talk about using forms in React. Forms are what you will build over and over again in your career!

You've seen and used forms in HTML. They're pretty simple and easy to use. A form that takes someone's name looks like this:

  ```html
  <form>
    <label>
      Name:
      <input type="text" name="name" />
    </label>
    <input type="submit" value="Submit" />
  </form>
  ```

In HTML, the elements like: `<input>`, `<textarea>`, and `<select>` handle their own state, but in React we want state to be handled in our component’s local state. We call this a **single source of truth**. When a React component that renders a form also controls what happens inside its form based on what the user inputs, we call it a **controlled component**. As the user types, the new state is set with the values they input and the value they see inside the form only represents what is stored in the component’s state. The code snippet below demonstrates a simple **controlled component**.

=== "Simple Controlled Component"

    ```javascript
    class NameForm extends React.Component {
      constructor(props) {
        super(props);
        // initialize the state with empty quotes ''
        this.state = {
          value: ''
          };

        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSubmit.bind(this);
      }

      // a method that, when called, changes the value of this.state.value
      handleChange(e) {
        this.setState({value: e.target.value});
      }

      // This method is called when the form is submitted. Potentially an API 
        // request could go here using the data from this.state .
      handleSubmit(e) {
        // Always put this line in on submits, it prevents the page from 
          // reloading and wiping your state.
        e.preventDefault();
        alert('A name was submitted: ' + this.state.value);
        // after doing something with the data we reset the form value to 
          // empty quotes again.
        this.setState({value: ''})
      }

      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              Name:
              {/* the value of the input is tied to this.state.value so 
              when a user types the handleChange method changes 
              `this.state.value` to match*/}
              <input 
                type="text" 
                value={this.state.value} 
                onChange={this.handleChange} 
              />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }  
    ```

=== "w/o comments"

    ```javascript
    class NameForm extends React.Component {
      constructor(props) {
        super(props)

        this.state = {
          value: ''
          };

        this.handleChange = this.handleChange.bind(this)
        this.handleSubmit = this.handleSubmit.bind(this)
      }

      handleChange(e) {
        this.setState({value: e.target.value})
      }

      handleSubmit(e) {
        e.preventDefault()
        alert('A name was submitted: ' + this.state.value)
        this.setState({value: ''})
      }

      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              Name:
              <input 
                type="text" 
                value={this.state.value} 
                onChange={this.handleChange} 
              />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    } 
    ```

In this way, we can control what data is sent off and when it is sent. Before moving on, make sure you read over all the examples laid out in the very clear [React Form Docs](https://reactjs.org/docs/forms.html). Pay special attention to the `<select/>` and [Handling Multiple Inputs](https://reactjs.org/docs/forms.html#handling-multiple-inputs).

### See It - Forms in React
<!-- ! Video Contents: Vimeo, Clayton@ACA - FormsInReact+BonusBinding - 411.1.1.* -->
<iframe src="https://player.vimeo.com/video/492122362" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## DRY Methods + Handle Submit

<!-- ! Video Contents: Vimeo, Clayton@ACA - DRY Methods + Handle Submit - 411.1.1.* -->
<iframe src="https://player.vimeo.com/video/492134939" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Practice It

This CodePen is the same code snippet you saw on the previous page. It was created by Dan Abramov the creator of Redux, a technology you'll learn in a few short weeks!

[Forms in React CodePen](https://codepen.io/gaearon/pen/VmmPgp?editors=0010)

### Instructions

- [ ] Open and fork the CodePen above
- [ ] Create 5 more text inputs: `lastname`, `DOB`, `age, pho`ne, and `gender` in this form.
- [ ] Use a `<select>` input for gender.
- [ ] Create keys in `this.state` to change the values based on what the user puts in.
- [ ] Console.log on submission.
- [ ] Now create an array in `this.state` that you can push into when the submit button is clicked.
- [ ] map over the array and display the users.

## Filter By Search Term

<!-- ! Video Contents: Vimeo, Clayton@ACA - FilterBySearchTerm - 411.1.1.* -->
<iframe src="https://player.vimeo.com/video/492146904" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Know Your Docs

- [ ] [Legacy React Docs - Forms](https://reactjs.org/docs/forms.html)
- [ ] [Legacy React Docs - Handling Multiple Inputs](https://reactjs.org/docs/forms.html#handling-multiple-inputs)

<hr>

- [ ] [React Dev Docs - Forms](https://react.dev/reference/react-dom/components/form#noun-labs-1201738-(2))
- [ ] [React Dev Docs - Reacting to Input w/state](https://react.dev/learn/reacting-to-input-with-state)


<!-- ! END OF VIDEO 101.1.3.1 - TITLE-->
<!-- ? Video Numbering and Title system: CourseNumber.ModuleNumber.LessonNumber.VideoNumber -->
<!-- * (VIDEO 101.2.4.3 - "CSS Selectors") === 101 Course, Module 2, Lesson 4, Video 3 - "CSS Selectors" -->
<!-- ! Video Contents:  width="655" height="368" -->

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