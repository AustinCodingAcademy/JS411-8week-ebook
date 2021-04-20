# Class 4: Hackathon

<!-- ! HIDE FROM STUDENT; INSTRUCTOR ONLY CONTENT -->
<!-- ## Instructor Only Content - HIDE FROM STUDENTS -->
<!-- cp workspace/resources/classOutlineTemplate.md docs/module- -->
*****
*****

## Instructor Notes

### What

* In-Class Hackathon to build a Hacker News Clone with the Algolia API.

* Groups of 3 - 4

* Architecture: 4 Components passing props

* Plan It => Build It => Evaluate It => Host It

### Why

* Need to internalize how to plan an app, visualize the needs and building blocks.

* Learn to read docs on their own.

* Work as a team.

* Organize on Trello and Git Branches

### How

* Divide the groups by partnering students by strengths.

* Require them to create a Trello board meanwhile one student can build a repo.

* Let them lead the planning but make sure they all have a plan before setting off.

* Let them lead their groups and mentor only when they ask.

* Watch the overview [video](https://vimeo.com/492160010).

<!-- ! END INSTRUCTOR ONLY CONTENT -->

*****
*****

*Wake up with determination. Go to bed with satisfaction.*

## Greet, Outline, and Objectify

<!-- SMART: Specific, Measurable, Attainable, Relevant, and Timely. -->
<!-- https://examples.yourdictionary.com/well-written-examples-of-learning-objectives.html -->
  
*OBJECTIVE: Today the student will learn and practice to understand:*

* *Developing an app in collaboration*
* *API requests, conditional rendering, mapping, forms*

*****

- [ ] Questions for Student Led Discussion
- [ ] Interview Challenge
- [ ] Student Presentations
- [ ] Creation Time
    * [ ] Hackernews Client or GitHub Issue Client
- [ ] Interview Questions: Blog to Show You Know
- [ ] Exit Recap, Attendance, and Reminders

### Questions for Student Led Discussion, 15 mins
<!-- This section should be structured with the 5E model: https://lesley.edu/article/empowering-students-the-5e-model-explained -->

[Questions to prompt discussion](./../additionalResources/questionsForDiscussion/qfd-class-4.md)

### Interview Challenge, 15 mins
<!-- The last two E happen here: elaborate and evaluate  -->
<!-- this sections should have a challenge that can be solved with the skills they've learned since their last class. -->
<!-- ! HIDDEN CONTENT: INSTRUCTOR ONLY -->
[See Your Challenge Here](./../additionalResources/interviewChallenges.md)
<!-- ! END HIDDEN CONTENT: INSTRUCTOR ONLY -->

### Student Presentations, 15 mins

[See Student Presentations List](./../additionalResources/studentPresentations.md)

## Creation Time, 60-90 mins

Today you will work with a team of 2-3 junior developers to build a Hackernews Client. For this Hackathon you will need to look at your available data and plan how you want to render it, then plan with your team how to build it. Work smart, not hard.

<iframe src="https://player.vimeo.com/video/492160010?color=2565EF&byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/492160010">411-22-HackathonOverview</a> from <a href="https://vimeo.com/zollege">Zollege</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

Here’s the regular Hacker News site, and then there’s the [Algolia Hacker News Search](https://hn.algolia.com/?dateRange=last24h&page=0&prefix=false&query=&sort=byDate&type=story). If you haven't visited either one, you should start bringing it into your daily practice.

It has been said that all web apps are basically just lists. This app will give you some practice with lists of components that are a little more complicated than todos.

Fetch stories from the [Algolia HN Search REST API](https://hn.algolia.com/api). Hint: Look under the Search heading.

### Instructions

- [ ] [Example NewsFeed](https://hn.algolia.com/?query=&sort=byPopularity&prefix&page=0&dateRange=all&type=story)

In groups of 2 - 3:

- [ ] Use your browser to see what the data looks like when you fetch it.
- [ ] Whiteboard and make a plan of the app you want to build with the data.
- [ ] Create a react app, git init and push it to a new repo, then git clone.
- [ ] Together, build a new app people can use!!
- [ ] Specs:

    * [ ] Starts with empty list
    * [ ] Has search bar at the top to filter search for terms
    * [ ] Accepts a search term and calls the HN API with that term as the query
    * [ ] Loads the list
    * [ ] Has a form input to search by date and author

- [ ] Follow-up: [Blog, Medium - How to Build a Simple Hackernews Feed](https://medium.com/styled-components/how-to-build-a-simple-hackernews-feed-with-styled-components-a8905211e45e)

### Push Yourself Further

- [ ] Add a "View Later" button to flag articles you want to read later. This will move the article into another list.
- [ ] Add a "Not Interested" section to flag articles you don't want to read and greys out the title text when clicked.
- [ ] Add functionality that only displays 10 articles at a time.

<!-- 
Optional Project Two

Make a simplified version of GitHub’s Issues page. Keep the scope small, just focus on implementing the list of issues, and ignore the stuff in the header (search, filtering, stars, etc).

Use the [GitHub Issues API](https://developer.github.com/v3/issues/)

Example of [GitHub Issues Tracker](https://github.com/facebook/create-react-app/issues)
Project 2 Instructions
In groups of 2 - 3:

- [ ] Use your browser to see what the data looks like when you fetch it.
- [ ] Whiteboard and make a plan of the app you want to build with the data.
- [ ] Create a React app, git init and push it to a new repo, then git clone.
- [ ] together, build a new app people can use!!
- [ ] Specs:
    * [ ] Has a form that:
    * [ ] Can filter by repo
    * [ ] Can filter by user.login
    * [ ] Can filter by state
    * [ ] Can filter by title 
 - [ ] Follow Up [Blog, GitHub - Issues Viewer](https://github.com/dceddia/github-issues-viewer)   
    
#### Push Yourself Further

- [ ] Add functionality that only allows you to see 10 issues at a time.
- [ ] Add a pagination control to allow navigating through the entire list of issues.

-->

## Blogs to Show You Know

[Blog Prompts](./../additionalResources/blogPrompts.md)

## Exit Recap, Attendance, and Reminders, 5 mins

- [ ] Create Hackathon Checkpoint Assignment
- [ ] Create Class 4 Blog Assignment
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