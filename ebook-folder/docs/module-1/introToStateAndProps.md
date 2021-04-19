# Intro to State and Props

*“The power of imagination makes us infinite.” —John Muir*

## Recap

Once you fall into React, you will fall in love with it. It's so simple and easy to use that you'll memorize all the life cycle methods and understand state and props and then you won't want to build with anything else. Today is going to be a whirlwind of facts and concepts. We're going to cover all the things that make up React. It'll be tough *at first* because it's a lot! And it's new to you. But rest assured, you will get enough practice with it in the coming weeks that all of it will sink in and you'll be proud to put React on your resume!

## Overview

Recall that React is a tool that helps us build **composable** websites and apps. This **composable** structure is the center-point to the whole mindset behind React. Each of the pieces on a website, the smaller components that make up the whole, are just that *components*. In 101 you were used to building the *components* of a web page with various HTML tags: `<article></article>`, `<p></p>`, etc. Each of these elements represented a small piece of the whole page.

With React we build functions that return these same elements. We call these functions **React Components**. The reason we build them as functions is that we might need to use the same element for an unknown amount of times with different data inside of it.

  > For example, on Facebook you have a page to view all of your friends. Each of your friends have different information but they are still displayed on the same element/piece/component with the same shape and styling.

  > Furthermore, you may have 6000 friends and I may only have 500. Using functions, the React app build by Facebook will call the FriendComponent function 6000 times when you look at your friends and 500 times when I look at my friends.

To make this work we need a way to pass unique data to each function call so that each function call will return the same HTML element but render the unique data we pass to it. This passing of data happens with something called `props` as in **prop**erties. You see, this `props` will be the *properties* of the element that is returned from the **React Component**(function).

## Props (How we pass data in React)

Below you'll see a code snippet of a couple **React components** (again, which are simple JavaScript functions!). The only thing that makes them "React" functions is that they can be passed to the much larger React function that ingests them and turns them into HTML elements on a web page, known as **React Elements**.

Just like functions, they can take arguments between their `()`. In fact, this is the only way we can pass `props`. To use the available **props** we must pass the `props` keyword into the `()` of the component.

=== "ChildComponent.js"

    ```javascript
      const ChildComponent = (props) => {
        return (
          <h1>`A ${props.propOne} tastes like ${props.propTwo}.`</h1>
        )
      }

      export default ChildComponent
    ```

  > In the above example you see the `props` keyword passed into the function as an argument right? Now where does the data associated with that `props` keyword come from?

Look what's going on here:

=== "ParentComponent.js"

    ```javascript
      class ParentComponent extends Component {
        constructor() {
        super();

        render() {
          <ChildComponent propOne={"I'm a "} propTwo={"Cutie Pie :)"}/>
        }
      }
    ```

In the code snippet above you see that our first `ChildComponent` is called inside our `ParentComponent`.

  > Notice the JSX syntax: When we call a component in React with JSX it looks a lot like HTML syntax?

In the line where we call the `ChildComponent` we see there are two props given: `propOne` and `propTwo`. They look a lot like attributes of an HTML tag, no? This is how we pass props down to other components. We can give them any attribute name we want. That same functionality could have been written: `<ChildComponent poop={"I'm a "} unicorn={"Cutie Pie :)"}/>`; but instead we choose useful attribute/property names.

Let's see it with `state` now. In the code snippet below we see the `ParentComponent` now has a `state` object, a simple JavaScript object with key and value pairs. Then we see the `ChildComponent` is called and passed props that reference keys of the `state` object. In this way we can pass local `state` to another piece/component of our application!!

=== "ParentComponent with state + ChildComponent"

    ```javascript
      class ParentComponent extends Component {
          constructor() {
          super();
          this.state = {
            pieceOne: 'fig newton',
            pieceTwo: 'garbage',
            pieceThree: 3500
          };

        render() {
          return(
            <ChildComponent propOne={this.state.pieceOne} propTwo={this.state.pieceTwo}/>
          )
        }
      }

      const ChildComponent = (props) => {
        return (
          <h1> `A ${this.props.propOne} tastes like ${this.props.propTwo}.` </h1>
        )
      }
    ```

If we want our parent component to pass down a piece of its `state` to a child component we give the child component attributes like `propTwo` then point it at the value we want: `propTwo={this.state.pieceTwo}`. After that we use the `props` keyword in the child component and presto! You have a component using **props**!! If we rendered `ChildComponent` it would say: `"A fig newton tastes like garbage."`

Under-the-hood, the `props` object would look like this:

```javascript
  props = {
    pieceOne: 'fig newton',
    pieceTwo: 'garbage'
  }
```

If you wanted to `console.log()` the value of the `pieceOne` key you would: `console.log(props.pieceOne)`.

```javascript
  const ChildComponent = (props) => {

    console.log(props.pieceOne)

    return (
      <h1> `A ${this.props.propOne} tastes like ${this.props.propTwo}.` </h1>
    )
  }
```

Hopefully that makes sense. If not, make sure you walk through it again so you can follow along with how the `props` are passed to components, then take a look at the following video and maybe that'll get you going in the right direction to build your own mental model of how data is passed from a parent component to any of its child components

### See & Practice

#### What Are Props

Follow the video below through to the challenge so you can:

- [ ] Visualize why props are needed in React.
- [ ] How they are used in the context of basic JavaScript's arguments & parameters.
- [ ] How to write the syntax of a new prop.
- [ ] And how to use props.


<!-- ! Video Contents: Vimeo, Clayton@ACA - What are Props - 411.1.2.1* -->
<iframe src="https://player.vimeo.com/video/491856368" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

#### How to Pass Props

Follow along with the video below so you too can:

- [ ] Create a new functional component.
- [ ] Import and export the component.
- [ ] Pass props to the new component.
- [ ] Squash a bug while exporting.
- [ ] And render your to-do list with the new component.

<!-- ! Video Contents: Vimeo, Clayton@ACA - Passing Props - 411.1.2.2* -->
<iframe src="https://player.vimeo.com/video/491859142" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

#### Passing Methods as Props (How to Remove your ToDos)

Following the "Three Jobs of a Developer", this vides shows you how to:

- [ ] Build a method to handle the deletion or *manipulation* and *moving of data* when we want to remove a to-do item.
- [ ] Pass a method as a prop to be used when the human-user clicks a button they can *see*.
- [ ] Finally, remove the item from where it is *stored* in state and *rendered* back to the user.

  > NOTE: "Three Jobs of a Developer": Store data, Move & Manipulate data, Show data to a human-user.

<!-- ! Video Contents: Vimeo, Clayton@ACA - Deleting a ToDo - 411.1.2.3* -->
<iframe src="https://player.vimeo.com/video/491865067" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

#### Destructuring Props

This video shows you how to **D.R.Y.** your code up by **destructuring** your props.

<!-- ! Video Contents: Vimeo, Clayton@ACA - Destructuring Props + Styling - 411.1.2.4* -->
<iframe src="https://player.vimeo.com/video/491869849" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Additional Resources

- [ ] [YT, Academind - React Basics #6: Passing Data w/Props](https://youtu.be/GIU8ekYndKw)

## Know Your Docs

- [ ] [React Docs - Props](https://reactjs.org/docs/components-and-props.html)
