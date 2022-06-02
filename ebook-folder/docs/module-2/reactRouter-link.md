# Creating Links to Update the URL

## Overview

This BrowserRouter is pretty cool because it uses a Router component to route the view to a specific component according to the URL, but how does the URL get changed?

## Using Link

Since Web 101 you've know that an `<a>` (anchor) tag is used to create hyperlinks on your site to get to a certain page in your website's folder, which typically look like this: `<a href="/dash">Go to Dashboard</a>`.

React Router provides its own linking mechanism that ensures interaction with our `<Router>` and `<Routes>` paths we created at the beginning of the homework. One of the great things about this component is that we can use it anywhere in our code. To do so, we need to import it first: `import { Link } from 'react-router-dom'`. (Maybe you're picking up on the pattern now?)

Once imported we can use it in our code like this:

=== "SomeComponent.js"

    ```javascript
    // ...some import statements
    import { Link } from 'react-router-dom'
    // ...more import statements

    // Now just write in the Link component, tell it where "to" route and give it some text
    const SomeComponent = (props) => {
        <div>
            <h1>Welcome to the SomeComponent Page</h1>
            <p>
                There's lots to do and see here
                but if you want the full range of
                capabilities provided by this App,
                you need to checkout the
                <Link to="/dash">Dashboard Page</Link>
                .
            <p>
        </div>
    }
    ```

Now, when a user clicks on the Dashboard Page link, the URL in the address bar will change, which will be picked up by the `BrowserRouter` component, which then calls the `Router` so the `<Routes>` component in the Router will return the correct component to the `<BrowserRouter>` —in this case, `<Dashboard/>`. The Link component at its simplest, just takes a prop called `to` which represents the path you want to navigate *to*.

  > EXTRA: You won't need this for tomorrow, but it's important to know that Links can send an object of properties through the `to` prop which makes them even more powerful. Take a look below:

=== "Example of Assigning an Object to the `to` prop in Link"

    ```javascript
    <Link
      to={{
          pathname: "/dash",
          search: "?sort=name",
          hash: "#the-hash",
          state: { fromHome: true }
      }}
    />
    ```

> NOTE: We generally won't need this much flexibility but it's important to note the power of the Link component. You can read more about it at [ReactTraining-Link](https://github.com/ReactTraining/react-router/blob/master/packages/react-router-dom/docs/api/Link.md).

## Know Your Docs

- [ ] [React Training Docs - Link](https://reactrouter.com/docs/en/v6/components/link)
