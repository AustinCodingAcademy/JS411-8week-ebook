# Dynamic Rendering with .map()

## Overview

You've done this already but I think it's good to review it so you don't get hung up on a simple and avoidable bug in these next few projects. When we `.map()` over an array in React we must provide the callback function an index for its second argument.

The reason we have to do this is because React works to make our app fast and efficient by watching the actual DOM and comparing it to the virtual DOM. To do this it needs to have a way the identify one instance of a component to an other. When we give the callback function an index we are giving React the chance to apply a unique individual value to each of the nodes that will be created in the DOM tree by each instance of the component.

The value we give it is called a **key**. To give each of our items in the array a unique and individual key we assign it the value of the index in the callback function of the `.map()` method.

## Mapping - Key & Index

=== ".map Example with key `i` as 2nd argument"

    ```javascript
    const todos = [{title: "Feed Dog", status: "red"}, {title: "Walk Dog", status: "yellow"}, {title: "Pet Dog", status: "green"}]

    const todoItems = todos.map((item, i) =>
      <li key={i} className={item.status}>
        {item.title}
      </li>
    );
    ```

Above we see an example of using the index of the item in the array as the key, represented as `i`. This is [not the preferred way but is the fall-back option](https://reactjs.org/docs/lists-and-keys.html) if you don't have [another way to assign unique keys](https://medium.com/dev-genius/the-quicky-lazy-but-effective-way-to-create-unique-keys-for-react-elements-e45d574028a3). If the items came with id keys we could assign the key to `item.id` or even `item.email` instead. All that matters to React is that each element has a unique id so it can do its job of updated and rendering what, when, and where.

  > Note: See how we assigned the className to the status of the todo item. This is JSX syntax that means the same as classname in HTML.

### Map Over & Render Data
<!-- ! Video Contents: Vimeo, Clayton@ACA - Map Over & Render Data - 411.1.2.7 -->
<iframe src="https://player.vimeo.com/video/491885124" width="655" height="368"  frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

<!-- ! https://drive.google.com/file/d/1o-65eIj14qu9021-QfoZRgxi-UBYJpO_/view?usp=sharing -->

## Practice It

Continuing with the Todo app you built last class, you're going to pull out the pieces that represent each todo into a separate component. Then you will map over state and pass to each instance of the component the props they need to render the todo item, the delete button, the edit button and the urgency status.

### Instructions

- [ ] Before you get going make sure you install this most wonderful VS Code Extension: [Simple React Snippets](https://marketplace.visualstudio.com/items?itemName=burkeholland.simple-react-snippets).
- [ ] Continue with the app you built in the first class of 411.
- [ ] Make a code plan through whiteboarding what you need to do.
- [ ] The todoList component should map over the `this.state.todos` and return a todoItem component for each todo in the array.
- [ ] The `todoItem` should be passed props that include handlers like: `handleClick`, `handleChange`, `handleEdit`.
- [ ] The `todoItem` should have a `state` that maintains the urgency `status` that holds the values of `green`, `yellow` or `red`.
- [ ] The `todoItem` component should render the `background-color` of the text based on the status of the item.
- [ ] At the end your Todo list should look the same but function differently with the exception of the status colors.

## Additional Resources

- [ ] [YT, Codevolution - List Rendering](https://youtu.be/5s8Ol9uw-yM)
- [ ] [Blog, Medium - Quick and Lazy Way to Assign Unique Ids](https://medium.com/dev-genius/the-quicky-lazy-but-effective-way-to-create-unique-keys-for-react-elements-e45d574028a3)

## Know Your Docs

Most importantly, use the React Docs as your guide each time you build with React.

- [ ] [UUID Docs - Home Page](https://www.npmjs.com/package/uuid)
- [ ] [React Docs - Hooks](https://reactjs.org/docs/hooks-intro.html)
- [ ] [React Docs - Lists & Keys](https://reactjs.org/docs/lists-and-keys.html)

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