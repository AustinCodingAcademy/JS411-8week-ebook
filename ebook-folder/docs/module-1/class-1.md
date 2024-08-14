# Class 1: Todo App

<!-- ! HIDE FROM STUDENT; INSTRUCTOR ONLY CONTENT -->
<!-- ## Instructor Only Content - HIDE FROM STUDENTS -->

<!-- Whether you’re just starting out or you’ve been teaching for years, here is your first Tip for Teaching.

You’re a developer, you know how this stuff works, that’s not what you have to stress over. Instead, focus your attention on how the class will flow from beginning to end. What do the students do when they come in? How do you introduce yourself? How do you get them to introduce themselves? What’s the next step? And then? And then? How does the end of class look?

Use the textbook to prepare for class. Each lesson is laid out for you to open, conduct, and close class. Bring you’re style and flair to it but don’t re-create the wheel. After all, the students can see the textbook as well...

Once you’ve understood the flow of the class lesson ahead of you, write yourself an outline in a markdown file, pen & paper, or even on the whiteboard. Once you have this, breathe. You got this!

<iframe src="https://player.vimeo.com/video/493935213?color=2565EF&byline=0&portrait=0" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/493935213">411-InstructorNotes:PreCoursePrep</a> from <a href="https://vimeo.com/zollege">Zollege</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

NOTE: THIS SECTION IS ONLY VISIBLE BY THE INSTRUCTOR. -->

<!-- ! END INSTRUCTOR ONLY CONTENT -->

*The way to get started is to quit talking and begin doing. —Walt Disney*

## Greet, Outline, and Objectify

<!-- SMART: Specific, Measurable, Attainable, Relevant, and Timely. -->
<!-- https://examples.yourdictionary.com/well-written-examples-of-learning-objectives.html -->
  
*OBJECTIVE - Today the student will learn and practice to understand:*

* *how to use React to create a simple composable web app*
* *Demonstrate their ability to build a new todo app in React from recollection*

*****

- [ ] Questions for Student Led Discussion + Quick Intros
- [ ] Interview Challenge
- [ ] Student Presentations
- [ ] Creation Time: Repeat the Homework
    * [ ] Create-react-app
    * [ ] Add origin
    * [ ] Create a todo list app
- [ ] Push Yourself Further
- [ ] Exit Recap, Attendance, and Reminders

### Questions for Student-Led Discussion, 15 mins
<!-- This section should be structured with the 5E model: https://lesley.edu/article/empowering-students-the-5e-model-explained -->

[Questions to prompt discussion](./../additionalResources/questionsForDiscussion/qfd-class-1.md)

### Interview Challenge, 15 mins
<!-- The last two E happen here: elaborate and evaluate  -->
<!-- this sections should have a challenge that can be solved with the skills they've learned since their last class. -->
<!-- ! HIDDEN CONTENT: INSTRUCTOR ONLY -->
[See Your Challenge Here](./../additionalResources/interviewChallenges.md)
<!-- ! END HIDDEN CONTENT: INSTRUCTOR ONLY -->

### Student Presentations, 15 mins

[See Student Presentations List](./../additionalResources/studentPresentations.md)

## Creation Time, 60-90 mins

As usual, it is incredibly important that you read the pre-homework. If you haven't read the pre-homework and worked through the code-along video YOU WILL BE FAR BEHIND TODAY!!!
 
In the pre-homework, you should have downloaded create-react-app and spun up a create-react-app, built a button that changes state from true to false and then displayed the change of state. Today, we're going to continue that process and build a todo app with React!!


[Example Simple React Todo App](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_todo_list_beginning)

1. Create a new react app:

    - [ ] `npx create-react-app my-app-name-here`
    - [ ] `cd my-app-name-here`
    - [ ] `git init` and create a new repo
    - [ ] `push` it to the new repo in GitHub
    - [ ] `git remote add origin "https://github.com/your_github_username/$repo_name.git"`

2. Yank out all the unnecessary code and begin building your todo app

    - [ ] Create the `state` for your `app.js` the equal an object with the values: `{isClicked: false, todos: [], text: ''}` in it
    - [ ] Create a button and add an `onClickHandler` that uses `this.setState({})` to change the value of `isClicked` from `false` to `true` and `true` to `false`
    - [ ] Create an input field and an `onChangeHandler` function that changes the state of text: '' to the `e.target.value` `onChange` of the input field
    - [ ] Change your `onClickHandler` function to uses `this.setState({})` to set the value of text as the last value `todos: []`
    
    > Don't forget to spread the rest/`...` of the `todos`

    - [ ] Now clear `text` in the same function
    - [ ] Once you have `state` being changed properly create an element that can be used for each of the items in `todos: []`
    - [ ] Now `.map()` over todos and show each item in the DOM.
        
    > REMEMBER to give the callback function in `.map()` an index and provide that to each of the elements as a prop: key={index}

3. Create a button on each of the item elements and uses `this` and when clicked removes/deletes the item from `todos: []`

    - [ ]  **METHOD 1**: Passing Methods/Functions as Props. Use the following mix-and-match options to pass a delete method that uses `this.setState` to update `state` when the delete button is clicked, passing the `index` of the item back up to the component that handles `state`.

        | ref | Mix & Match Code Snippets |
        | - | - |
        | a | `handleClick={index => this.deleteItem(index)}` |
        | b | `delete = (index) => { ` |
        | c | `}` |
        | d | `let objectCopy = [...this.state.item]` |
        | e | `ObjectCopy.splice(index, 1)` |
        | f | `this.SetState({items: [...objectCopy]})` |
        | g | `<button onClick={() => props.handleClick(index)}>Delete</button>` |

    - [ ] Follow-up Video: [TY, Coding Addict - React Course: Todo List Project](https://youtu.be/8QBYrKhqgFI?feature=shared&t=3024)

    - [ ] Or use **METHOD 2**: use `setState` Hook - [https://www.robinwieruch.de/react-remove-item-from-list](https://www.robinwieruch.de/react-remove-item-from-list)

### Push Yourself Further

- [ ] Create a button that allows you to edit each todo
- [ ] [Add](https://medium.freecodecamp.org/reactjs-implement-drag-and-drop-feature-without-using-external-libraries-ad8994429f1a) a [drag and drop](https://react.rocks/tag/Drag_Drop) feature to reorder the todos
- [ ] Complete both methods of the delete and add functionality

## Student Feedback

<iframe src="https://docs.google.com/forms/d/e/1FAIpQLScjuL10i2xFGMWRwkjtgAL8F1Y5ipMPPjtTCDzkO1ZBcxUYZA/viewform?embedded=true" width="640" height="500" frameborder="0" marginheight="0" marginwidth="0">Loading…</iframe>

## Exit Recap, Attendance, and Reminders, 5 mins

- [ ] Prepare for next class by completing all of your pre-class lessons
- [ ] Complete the feedback survey(if applicable)

<!-- <iframe id="openedx-zollege" src="https://openedx.zollege.com/feedback" style="width: 100%; height: 500px; border: 0">Browser not compatible.</iframe>
<script src="https://openedx.zollege.com/assets/index.js" type="application/javascript"></script> -->

<!-- TODO Create 3 question exit questions -->

<!-- TODO INSERT Student Feedback From -->

<!-- TODO INSERT *HIDDEN* Instructor Feedback Form -->
