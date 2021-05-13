# Capstone App Planning

*Push yourself, because no one else is going to do it for you.*

## Overview

For the past few classes we've talked about how to connect the client (frontend) to a server (back-end API). This connection is essential to providing the user with data. Often times the data provided to users comes from many APIs. Perhaps your app provides the user with good hunting land entrances from the database you control but you'd also like to give them relevant weather conditions. To do that it would be best to use another's weather API such as [DarkSky](https://darksky.net/dev), [WeatherUnderground](https://www.wunderground.com/member/api-keys), or [others](https://rapidapi.com/blog/access-global-weather-data-with-these-weather-apis/). If you wanted other services like traffic, sunrise, water temps or water depth you'd need to bring in services from other APIs.

Perhaps you can start to see how these relatively small apps can become very large projects.

In the next few weeks you'll have class time dedicated to planning and building your Capstone App with the help of your instructor. It's important to understand that **planning** is more important than building/coding. Why? Because if you start coding your focus will be too narrow, just one line at a time. But if you start planning your focus is from higher up with an overview perspective of the app and you can make better decisions about what needs to done, when.

Once you've planned from this higher perspective you can zoom into specific problems as you need to code them out but zoom back out when you need to see everything as a whole. It would be wise to think of this zooming in and zooming out process as a necessary skill you must practice to be successful at building not only your app for graduation but also when building software for a client or your company.

## System Design

System design is the process of designing the elements of a system such as the architecture, modules and components, the different interfaces of those components and the data that goes through that system. System design is a high level view of what the application will look like, and how the application should work in the end.

### Read It - System Design

System design can be broken up into 3 categories: the client, services, and database. The client is what we will focus on today as you've already built most of your database and server in 311. It should also be stated that system design is not React specific, it is for all applications and for any library or framework you choose to build in.

These are some questions to consider when developing any client application.

What does my app actually do?
What core functions does my app perform to do this?
How will the user interact with the app?
How can I build the app so that it is scalable? This is to say, how can I plan to create variables to be referenced and reused by multiple parts of the system and how can I build components to be reused as much as possible?
Also, how can I can make my app responsive?
For a deeper understanding of System Design from a very high-level, read over this article on [10 Practical tips for Getting Your Clients Design System off to a Great Start](https://uxdesign.cc/10-practical-tips-for-getting-your-clients-design-system-off-to-a-great-start-7ac585dcc75d).

<!-- ! Video Contents: Vimeo, Clayton@ACA - TITLE - 411.1.1.* -->
<!-- <iframe src="https://player.vimeo.com/video/*" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe> -->

<!--
    === "title"

    ```javascript
    
    ```
    === "title"

    ```javascript
    
    ```
-->

### Practice It

On a sheet of paper, design a login component to an application (maybe the one you've built already?). The app will need to have a:

- [ ] Sign-on page
- [ ] Service that checks if user is in database
- [ ] A home page after the user is authorized

**Seriously**, take the time now to draw out on paper what the component looks like to the user. Then draw the services behind the component. Then draw the database. Now the server and the routes it will use to authorize the user. Then the logic of moving the user from the sign in to the home page. **It doesn't matter what it looks like so long as you actually did it.** The visualization of this process will help you build this in the future much, much faster!! And with less bugs and headaches

## Core Functionality

Today will you be your first day to work with a teammate and your instructor to begin planning your Capstone App. **Take the time now to WRITE your ideas, plan, functionalities, and diagrams out.** Your teammate will do the same thing and you both can work much faster.

In the next few classes and homeworks we'll work through steps for you to successfully and quickly build a Capstone App that demonstrates your programming abilities. Work through the first three now.

### Step 0: Pick an Idea, Pick a Partner

By now you should have a reasonable idea of an app you’d like to build for your Capstone Project. After all, you’ve been pitching to your classmates what you’d like to build and discussing with your instructors the app you’d like to build, and building a database for it. For these last two weeks of your 400 level class, it would be best to partner with someone else, especially if you like frontend and they like backend or vice versa. Working with someone else will prove hugely beneficial for your first web app. Which brings us to the first and main point: This is your first web app! You’re going to make mistakes. You’re going to want to [beat your head against the keyboard](http://giphygifs.s3.amazonaws.com/media/g8GfH3i5F0hby/200w_d.gif), you’re going to struggle, and you may even cry. All of this is part of the process. After this app you’ll have learned lessons you’ll want to carry on with you to your next app and your next job.

=== "Good Coding"

    <div style="width:100%;height:0;padding-bottom:56%;position:relative;"><iframe src="https://giphy.com/embed/ekjmhJUGHJm7FC4Juo" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div>

=== "Bad Coding"

    <div style="width:100%;height:0;padding-bottom:56%;position:relative;"><iframe src="https://giphy.com/embed/dlMIwDQAxXn1K" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div>

=== "No GIF"

    <!-- ![blank-black](./../images/blank-black.png) -->

What’s important now is that you commit yourself to building, mentally and physically! Below you’ll find a list of tasks for you to do that, if followed, will bring this figment of imagination in your mind to fruition, to the world, for all to see and use. You are about to embark on the truest gift of programmers: materializing previously unrealized ideas of solutions for the world to use.

### Step 1: List out the Core Functions of Your App

Now that you’ve decided on the app you want to build and the teammate you’d like to have for this courageous adventure, let’s list out the core features/functions of your app. To do this, think of the core functions of any app you use now like Twitter, Facebook, Reddit, SnapChat, YouTube, etc. For our sake, we’ll use Reddit.

#### Core Functions of Reddit

- [ ] users can create an account
- [ ] users can retrieve lost passwords
- [ ] users can change their passwords
- [ ] users can post new links
- [ ] users can comment on links
- [ ] users can upvote/downvote links
- [ ] users have a profile showing their history activity

While we could name a few other functions, we are only naming **CORE FUNCTIONALITY**. Please don’t stray away from these core functions. You are a beginner and all you need right now is to build your first app with simple **CORE** functionality. Once you’ve built each of the functions you and your teammate list out in this step you can add new features on top. **BUT NOT UNTIL AFTER YOU’VE BUILT THE CORE FUNCTIONS.**

For an example of an actual Capstone Project, we’ll use Budget App by Selena Solis and Nurzat Nijat. The purpose of this app was to easily translate and budget currency using the latest exchange rates for Nurzat, who just immigrated to the US and Selena who recently visited Iceland. At graduation, their app's functionality included:

- [ ] Users could create an account
- [ ] Users could sign in
- [ ] Users could create a budget
- [ ] Users could select the currency of their budget
- [ ] Users could enter an item and the cost in a specific currency

The user’s budget would be subtracted using the chosen currency
I’m sure after graduation they went on to add a few features like: multiple budgets, profiles, geolocation, password reset, and design. What’s important here is that the app was functional at its core. So should yours.

### Step 2: Simplify Your Core Functionality
s
Please, *please*, **please** take time to look at your “core functionality” and decide what you can cut. There are pieces that you’ve listed that could easily be implemented later. Ask your teammate to take a serious look at the function you want your app to perform and decide what can wait for later.

## Capstone App Requirements

Please refer to the [Graduation Prerequisites](./../additionalResources/graduationPrerequisites.md) for a complete list of requirements for your Graduation Presentation, Certification and Completion of this program.

*****
