# Class 2: Punk API Beer App

<!-- ! HIDE FROM STUDENT; INSTRUCTOR ONLY CONTENT -->
<!-- ## Instructor Only Content - HIDE FROM STUDENTS -->
<!-- cp workspace/resources/classOutlineTemplate.md docs/module- -->
<!-- ! END INSTRUCTOR ONLY CONTENT -->

*Your limitation—it’s only your imagination.*

## Greet, Outline, and Objectify

<!-- SMART: Specific, Measurable, Attainable, Relevant, and Timely. -->
<!-- https://examples.yourdictionary.com/well-written-examples-of-learning-objectives.html -->
  
*OBJECTIVE: Today the student will learn and practice to understand:*

* *passing data between components using props*
* *set state and use it*
* *fetch external data and set state with it*
* *dynamically render data with uniform elements*

*****

- [ ] Questions for Student-Led Discussion
- [ ] Interview Challenge
- [ ] Student Presentations
- [ ] Creation Time
    * [ ] Pair up to build in pairs
    * [ ] Plan your beer app (whiteboard & Code Plan)
    * [ ] Create a repo and program
- [ ] Push Yourself Further
- [ ] Interview Questions: Blog to Show You Know
- [ ] Exit Recap, Attendance, and Reminders

### Questions for Student-Led Discussion, 15 mins
<!-- This section should be structured with the 5E model: https://lesley.edu/article/empowering-students-the-5e-model-explained -->

[Questions to prompt discussion](./../additionalResources/questionsForDiscussion/qfd-class-2.md)

### Interview Challenge, 15 mins
<!-- The last two E happen here: elaborate and evaluate  -->
<!-- this sections should have a challenge that can be solved with the skills they've learned since their last class. -->
<!-- ! HIDDEN CONTENT: INSTRUCTOR ONLY -->
[See Your Challenge Here](./../additionalResources/interviewChallenges.md)
<!-- ! END HIDDEN CONTENT: INSTRUCTOR ONLY -->

### Student Presentations, 15 mins

[See Student Presentations List](./../additionalResources/studentPresentations.md)

## Creation Time, 60-90 mins

Build a simple app that requests information from the [https://www.openbrewerydb.org/](https://www.openbrewerydb.org/) and dynamically renders data from it with React components.

### Project Instructions

- [ ] Pair-program this one
- [ ] Create a react app: PUNK-API-REACT-APP
- [ ] `git init` and `push` it up as a repo
- [ ] In your `app.js` component make an HTTP request with `axios` to: [`https://www.openbrewerydb.org/`](https://api.punkapi.com/v2/beers) and set the data that comes back into an array in `state`.
- [ ] Build a brewery component that displays everything about the brewery using and `<iframe>` element to display the website of the brewery.
- [ ] Map over state and render a component for each brewery in state
- [ ] Add a button that allows a user to "like" a brewery

### Follow-up Video

- [ ] [YT, ihatetomatoes - React, How to use Fetch API](https://youtu.be/aNMY0lrWZXU)

### Push Yourself Further

- [ ] Create a collapsible list of all the beers of each brewery.
- [ ] Follow along with Peter Tichy at [ihatetomatoes](https://www.youtube.com/channel/UC7O6CntQoAI-wYyJxYiqNUg) through his [React Tutorial](https://www.youtube.com/playlist?list=PLkEZWD8wbltnXlfyhS5qSMTNb26utkOkI) to make the components of the app collapsible and interactive.
- [ ] Go find another API and build another React app: [https://apilist.fun](https://apilist.fun/)
- [ ] Build the functionality for your "liked" heart

<iframe src="https://player.vimeo.com/video/492109869" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<a href="https://player.vimeo.com/video/492109869"><p>411-16-Code Plan Your Like Button</p></a>

## Student Feedback

<iframe src="https://docs.google.com/forms/d/e/1FAIpQLScjuL10i2xFGMWRwkjtgAL8F1Y5ipMPPjtTCDzkO1ZBcxUYZA/viewform?embedded=true" width="640" height="500" frameborder="0" marginheight="0" marginwidth="0">Loading…</iframe>

## Blogs to Show You Know

[Blog Prompts](./../additionalResources/blogPrompts.md)

## Exit Recap, Attendance, and Reminders, 5 mins

- [ ] Create PunkAPI Assignment
- [ ] Create Class 2 Blog Assignment
- [ ] Before you give the attendance code, STOP everyone and hold a quick verbal review of these terms. Ask the class and let students call out the answer freely. Don't let only one student answer them all though!

    * [ ] Props
    * [ ] State
    * [ ] `setState()`
    * [ ] Template literals in JavaScript
    * [ ] Give attendance code

- [ ] Prepare for next by completing all of your pre-class lessons
- [ ] Complete the feedback survey
- [ ] Record every class.
- [ ] Remind the students to merge their PRs (if applicable).
- [ ] Remind students to bring paper and pencils to every class for whiteboarding.

<!-- <iframe id="openedx-zollege" src="https://openedx.zollege.com/feedback" style="width: 100%; height: 500px; border: 0">Browser not compatible.</iframe>
<script src="https://openedx.zollege.com/assets/index.js" type="application/javascript"></script> -->


<!-- TODO Create 3 question exit questions -->

<!-- TODO INSERT Student Feedback From -->

<!-- TODO INSERT *HIDDEN* Instructor Feedback Form -->

<!-- 
height/width = 1.777 ---- width="655" height="368"
cp workspace/resources/classOutlineTemplate.md docs/module-
 -->