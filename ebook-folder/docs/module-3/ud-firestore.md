# **_U_**pdate and **_D_**elete - Firestore

## Overview

In this sections, we will be covering the last two operations of a **_"CRUD"_** application, **_U_**pdate and **_D_**elete. As of know, we are only familiar with **Reading** and **Creating** data, but we also want to allow the user to **Update** or **Delete** this data as needed, some data doesn't always stay the same, after all.

Let's say for example, a user **created** a book **document** but misspelled the title. Well, we want the user to be able to **edit** this error and **update** our **collection**. Maybe the user just wants to **delete** the **document** as a whole? Well they should be able to **delete** the data as well.

We will begin with **delete**, as it is a bit simpler, and then move on to **update**.

## **_D_**elete

So to **delete** a **document** from our Firestore DB, we need to bring in a couple of functions from the **firebase/firestore** library. We will be importing `{ doc, deleteDoc }` from `"firebase/firestore"`. Make sure to also import the **db** instance from our **config** file.

Follow along in the example below. We begin with a higher overview followed by an example for React.

=== "Deleting a Document - Overview"

    ```javascript
    // import our 'db' instance from our 'config' file
    import { db } from "../firebase/config";

    // import doc and deleteDoc from 'firebase/firestore
    import { doc, deleteDoc } from "firebase/firestore";

    // `deleteDoc` will take one parameter, the document reference provided by
    // `doc`. `doc` will take 3 parameters: our db instance, the collection to
    // reference, and a Unique Identifier. We will wait for the results.
    await deleteDoc(doc(db, "books", id));

    // See next slide to see a more robust example using React...

    ```

=== "Delete - React Example"

    ```javascript
    import React, { useState } from "react";
    import { db } from "../firebase/config";
    import { doc, deleteDoc } from "firebase/firestore";

    const List = (props) => {

      // Let's assume we already have our data and we are passing it in as
      // props to our List component and setting our state here.
      const [data, setData] = useState(props.data)

      // We will handle our delete document event in this function, this is
      // being called by the onClick property on Line 26
      const handleDelete = async (id) => {

        // We make a request to Firestore to delete a specific document by id
        await deleteDoc(doc(db, "books", id));

        // We also want to update our current state to reflect the changes
        // we have made. We will use filter here to update our state instead
        // of making an unnecessary request to Firestore.
        const newData = data.filter((item) => item.id !== id)

        // Set the data of our new updated Array an re-render the component.
        setData(newData)
    };

    return (
      {/* This is a simple example, style as necessary or implement MUI */}
      <div>
        <ul>
          {data.map((item) => (
            <li key={item.id}>
                {item.title}
                <span>
                  {/* This button has our event handler  */}
                  <button onClick={handleDelete}>X</button>
                </span>
            </li>
          ))}
        </ul>
      </div>
    );
    }

    export default List;
    ```

There you go, it's that simple! Deleting a specific document is one of the easier operations and does not require much to implement. As long as you update the state properly, your component should reflect that of our database.

You can always make another request to the DB to get an updated list, but if we can avoid unnecessary requests, we will always opt for that. Remember, data costs money, so do making requests. Although we, hopefully, won't make enough requests to go over the the free tier limit, it is always best practice to minimize any extra work our app needs to do.

There are other ways to delete data from our Firestore DB, make sure you check out the [Firebase Documentation about Deleting data]("https://firebase.google.com/docs/firestore/manage-data/delete-data) if you are interested in deleting a collection or maybe just specific fields in a document.

Next, let's talk about updating data.

## **_U_**pdate

We have finally arrived at to ***U***pdating data. By now, we have learned to create, read, and delete data, and hopefully we still have some data to update. To update a document, we need to bring in two functions from the "firebase/firestore" library. We need to import `doc` to create a reference to specific document by it's ID. To create that reference, we need to provide the `doc` function our `db` instance, the collection the document exists in, and last, the ID the document has. 

It is possible for this ID to come dynamically from maybe `react-router-dom`, using the `useParams` or `useLocation` method, or maybe by passing along props to a "Edit" component, or by many other ways. In these examples, we are going to hardcode an ID that we know exists in our Firestore DB. If you are following along, make sure to go to your Firestore DB and get an existing ID from your *book* collection to use in the React example below.

First, we will begin with a high overview, followed by a somewhat complex React example that includes a `getDocs` function called inside a useEffect to get us the data we want to edit. We also talk about Timestamp a little more in depth in this section as well as the "date" type input. There is a lot going on here, so make sure to go over it slowly.

=== "Updating a document - Overview"

    ```javascript
    // As always, import the db instance
    import { db } from "../firebase/config";
    
    //import these functions from `firebase/firestore` library
    import { doc, updateDoc } from "firebase/firestore";

    // Create a reference to the document you want to update. The `doc` function
    // will take in 3 parameters: the `db` instance, the collection we want to
    // reference, and the ID of the specific document we want to update.
    const documentRef = doc(db, "books", "UniqueID123"); {/* Document ID */}

    // We await the results of `updateDoc`. `updateDoc` will take in two 
    // parameters: the document reference and the fields we want to update.
    await updateDoc(documentRef, {
      title: "Lord of the Rings: The Two Towers",
      author: "J. R. R. Tolkien",
      publish_date: Timestamp.fromDate(new Date("1954-07-27")),
      characters: ["Frodo", "Gandalf", "Smeagol"]
    })

    // If you look back at the "Create" example, you can see I am updating this 
    // current document with a new title and a new character, while the date 
    // stays the same.

    // Firestore will only update the Fields mentioned in the object and will 
    // not overwrite any existing data that is not mentioned.

    // Check next slide for an example in React.
    ```

    >Note: Although you can update data by specifying fields to update, it is normal convention to include all fields in the document when creating a client-side "edit" form. In order to do so, you want to make sure you have the documents current data and lay them out in the input fields provided to the user. By doing this, you are preemptively assuring all data is capable of being edited and returned properly to the DB. Even if the user doesn't specifically edit all of the fields, we will be sure that we will still be getting back the same data along with any new data.

=== "Updating a document - React Example"
    
    This is a bigger example, so try to follow along as best you can. We are going to request some data from our Firestore DB so that we can edit it. To this, we need to have a document and it's ID to reference that document. We can do this by copying it from the collection on the Firestore console. For this, we are also going to need to `import {getDoc} from "firebase/firestore"`. `getDoc` will allow us to get a single document, where `getDocs`, another method we previously used in the ***R***ead example, will get all the documents in a collection. We are also going to import `{Timestamp} from 'firebase/firestore' as the *Timestamp* constructor will allow us to format a basic Date string into a Firestore timestamp. We will talk a little more about this timestamp as we go through this example.

    ```javascript
    import React, { useEffect, useState } from "react";
    // Make sure to include all the imports needed in this component
    import { doc, updateDoc, getDoc, Timestamp } from "firebase/firestore";
    // This is a function in another example we are going to use to format a
    // date. Please look at that example to get a better understanding.
    import dateTypeFormat from "../util/dateTypeFormat";
    // Also, there is a css sheet example you can use as a template that works
    // with this component. The classnames have already been created.
    import "./styles.css";

    const Edit = () => {
      // Set our body to null at initial render, we will set data later
      const [body, setBody] = useState(null);

      // This state will help us push character names items into an array
      const [character, setCharacter] = useState("");

      // We will useEffect here to request data by it's ID from Firestore
      useEffect(() => {
        // We create an asynchronous function here since we will have to
        // wait for our results from Firestore.
        const getDocument = async () => {
          // Create the reference to a document, include your ID here
          const documentRef = doc(db, "books", "BOOK_ID_HERE");
          // "await" the results from "getDoc" and assign the results to
          // a variable called "document"
          const docResults = await getDoc(documentRef);
          // Check if a document exists with that ID. We use the ".exists()"
          // function that comes from our result, remember, the Firestore 
          // results will be an object with different fields we can use, 
          // including functions. 
          if (!docResults.exists()) return console.log("Document doesn't exist");
          // Now, lets some our body data from our results
          setBody({
            // We want to include the documents ID from the results
            id: docResults.id,
            // We call the ".data()" function that comes from our results.
            // This is where we get the actual document, by call this function.
            // We use the "..." spread operator to lay the fields from our
            // document into this object we are creating
            ...docResults.data(),
            // Format the data, please see the "dateTypeFormat" example. Pass
            // a date into the "dateTypeFormat()" function. This date is a 
            // Firestore Timestamp which is an object which we need to convert
            // to a readable string for us to use properly. The ".toDate()"
            // function turns our date into a JS Date object which we then
            // call the JS method ".toLocaleDateString()"to extract only the
            // date which looks like this "07/07/2020".
            publish_date: dateTypeFormat(
              docResults.data().publish_date.toDate().toLocaleDateString()
            ),
          });
          // The "body" state should look like this at this point:
          // {
          //   id: "65fds6a+56s", 
          //   title:"Some Book",
          //   author:"Some Author",
          //   publish_date: "2020-07-07"
          //   characters: ["Character 1", "Character 2", ...]
          // }
        };
        // We need to call the async function we just created
        getDocument();
        // We leave the dependency array empty to prevent an infinite loop
      }, []);

      // This event handler function will allow us to "push" a string to our
      // characters array inside our body.
      const addToArrayHandler = () => {
        // Copy current state and assign object to a variable "newBody"
        const newBody = { ...body };
        // Use dot-notation to get the characters array and push new character
        newBody.characters.push(character);
        // set our "body" state with our "newBody" object we created with our
        // new data.
        setBody(newBody);
        // Set the character state to an empty string to await another input
        setCharacter("");
      };

      // This event handler function is similar since we are also making a
      // shallow copy of our current state and updating it with new data.
      // Except the new data will be the removal of a character inside our
      // characters array. We pass the character "string" as "item" in the
      // parameter.
      cont deleteFromArrayHandler = (item) => {
        const newBody = { ...body };
        // We use the .filter method here to filter our array to all our
        // character "strings" that do not match the character item "string 
        // we want to remove. Returns a new array.
        const newArr = newBody.characters.filter((i) => i !== item);
        // Replace the characters array in our newBody with our new Array
        newBody.characters = newArr;
        // Push that new body into our body "state"
        return setBody(newBody);
      };

      // This event handler function just takes care of a user pressing enter
      // when inside our add character input field. It prevents it from
      // submitting the form completely, while still adding the character 
      // and emptying the input. We pass the event in the parameter
      const handleEnter = (e) => {
        // If the key pressed is "Enter"
        if (e.key === "Enter") {
          // Prevent the default behavior of pressing "Enter"
          e.preventDefault();
          // Call our "addToArray" function from above to do the same work
          addToArrayHandler();
        }
      };

      // Finally, this function takes care of actually updating our document.
      // We pass in the event in the parameter, again, to prevent default 
      // behavior from the form when we "submit" it.
      const handleSubmit = (e) => {
        e.preventDefault();
        // Create the reference to the specific document we want to update.
        // This will include the ID of the document we have stored inside
        // the body "state"
        const docRef = doc(db, "books", body.id);
        // Await the result from "updateDoc", this function takes in our
        // document reference and an object with the fields we are updating
        // in the document. We are using the "..." spread operator to lay 
        // all the fields in our body 'state' into this object.
        await updateDoc(docRef, {
          ...body,
          // We do need format our date again to be a Firestore Timestamp
          // We call our Timestamp constructor, call the "fromDate" from the
          // Timestamp object, and then create a "new Date" with our date string 
          // from our body "state". 
          publish_date: Timestamp.fromDate(new Date(body.publish_date)),
        });
      };

      // We want to render a message that says "loading..." while our
      // useEffect is making the query to our Firestore DB. While body
      // is still null, we get this message. Now, if you never get the 
      // actual data, it is possible a document with that ID doesn't exist.
      if(!body){
        return <p>"loading..."</p>
      }

      // Once body actually has our data, we render our actual page details.
      // Look through the form and understand how it all works. You can see
      // certain inputs have certain events calling the functions above. 
      return (
        <div className="edit_container">
          <h3 className="edit_title">Edit Book</h3>
          <form onSubmit={handleSubmit} className="edit_form">
            <label>
              Title:
              <input 
                type="text" 
                value={body.title} 
                onChange={(e) => {
                  setBody({ ...body, title: e.target.value });
                }}
              />
            </label>
            <label>
              Author:
              <input 
                type="text" 
                value={body.author} 
                onChange={(e) => {
                  setBody({ ...body, author: e.target.value });
                }}
              />
            </label>
            <label>
              Date:
              <input
                type="date"
                value={body.publish_date}
                onChange={(e) => {
                  setBody({ ...body, publish_date: e.target.value });
                }}
              />
            </label>
            <label>
              Add a Character:
              <span className="add_character_container">
                <input
                  type="text"
                  value={character}
                  onKeyPress={handleEnter}
                  onChange={(e) => setCharacter(e.target.value)}
                />
                <button type="button" onClick={addToArrayHandler}>
                  Add
                </button>
              </span>
            </label>
            Character List:
            <ol className="character_list_container">
              {body.characters.map((item, index) => (
                <li key={index} className="character_item">
                  {item}
                  <button
                    type="button"
                    onClick={() => deleteFromArrayHandler(item)}
                    className="remove_character_btn"
                  >
                    X
                  </button>
                </li>
              ))}
            </ol>
            <button type="submit">Submit</button>
          </form>
        </div>
      );
    };

    export default Edit;
    ```

=== "Date Type Input (Date Format) - Function Example"
    This function is in charge of changing the format of our date to fit that of an input with the type of "date".

    Why is this important? Well, when we update a document, we want to provide all current data inside the document. We can fill our inputs to have these values already and the user will simply change what needs to be changed and send the whole document back up to update. If we are working with Timestamps, we have to convert that data to a readable format, and break it down even further to be readable by the date input.
    
    The date input will return a string in the format of "2014-06-05". When we get our Timestamp from Firestore, and convert to a string using the "toDate() function, we get a readable date, but we still need to convert this to an even more readable string and also extract the date specifically. We use a JS method called `.toLocaleDateString()` to get back the date in string format. Ex. "6/5/2014".

    We will take a quick look at the example we used earlier.

    ```javascript
        docResults.data().publish_date.toDate().toLocaleDateString()
        // This returns the string in "6/5/2014". Let's break it down
        
        docResults.data().publish_date
        // returns {seconds: 1402012800, nanoseconds: 0}
        
        docResults.data().publish_date.toDate()
        // returns "Thu Jun 05 2014 19:00:00 GMT-0500 (Central Daylight Time)"
        
        docResults.data().publish_date.toDate().toLocaleDateString()
        // finally we get this result: "6/5/2014"
        
    ```

    You would expect that to be enough, but remember, the date input format is "2014-06-05", and yes, even the 0's matter as well as the year placement. 

    Since, "2014-06-05" is not the same format as "6/5/2014", if we try to provide a value to the date input without formatting it, we get an error saying:

    ```console
      The specified value "6/5/2014" does not conform to the required format, "yyyy-MM-dd"
    ```
    In order for a date input to have a default value, we need to format our string to be the format it expects it to be, which is why we have this helper function. Feel free to use it if you decide Timestamps are for you!

    ```javascript
    const dateTypeFormat = (date) => {
      let newDate = date.split("/");
      const year = newDate.pop();
      newDate.unshift(year);
      if (newDate[1].length < 2) {
        newDate[1] = "0" + newDate[1];
      }
      if (newDate[2].length < 2) {
        newDate[2] = "0" + newDate[2];
      }
      newDate = newDate.join("-");
      console.log(newDate);
      return newDate;
    };

    export default dateTypeFormat
    ```
    Now all this can be completely unnecessary and entirely up to you. Of course, at the end of the day, you could always just save the date in a string instead of a Timestamp... but where is the fun in that?

=== "Styles - CSS"

    Here are some included css styles if you take the large snippet from this book. Feel free to change it more to your styles, it is a good template to start with, especially for demonstration purposes.

    In your actual project, feel free to use MUI instead.

    ```css
    .edit_container {
      margin: auto;
      width: 250px;
      padding: 10px;
      border: 1px black solid;
      border-radius: 10px;
      box-shadow: 2px 2px 6px;
    }

    .edit_title {
      text-align: center;
    }

    .edit_form {
      display: flex;
      flex-direction: column;
      margin: auto;
      gap: 10px;
    }

    .edit_form input {
      box-sizing: border-box;
      width: 100%;
    }

    .add_character_container {
      display: flex;
    }

    .character_list_container {
      display: flex;
      flex-wrap: wrap;
      padding: 0;
      margin: 0;
    }

    .character_item {
      background-color: gray;
      margin: 2px;
      border-radius: 16px;
      list-style: none;
      padding: 5px;
      font-size: 14px;
      display: flex;
      align-items: center;
    }

    .remove_character_btn {
      text-align: center;
      width: 13px;
      height: 13px;
      border-radius: 50%;
      border: 0;
      padding: 0;
      font-size: 10px;
      margin-left: 3px;
      cursor: pointer;
    }

    ```
=== "React Example - Clean Version"

    ```javascript
    import React, { useEffect, useState } from "react";
    import { doc, updateDoc, getDoc, Timestamp } from "firebase/firestore";
    import dateTypeFormat from "../util/dateTypeFormat";
    import "./styles.css";

    const Edit = () => {
      const [body, setBody] = useState(null);

      const [character, setCharacter] = useState("");

      useEffect(() => {
        const getDocument = async () => {
          const documentRef = doc(db, "books", "BOOK_ID_HERE");
          const docResults = await getDoc(documentRef);
          if (!docResults.exists()) return console.log("Document doesn't exist");
          setBody({
            id: docResults.id,
            ...docResults.data(),
            publish_date: dateTypeFormat(
              docResults.data().publish_date.toDate().toLocaleDateString()
            ),
          });
        };
        getDocument();
      }, []);

      const addToArrayHandler = () => {
        const newBody = { ...body };
        newBody.characters.push(character);
        setBody(newBody);
        setCharacter("");
      };

      const deleteFromArrayHandler = (item) => {
        const newBody = { ...body };
        const newArr = newBody.characters.filter((i) => i !== item);
        newBody.characters = newArr;
        return setBody(newBody);
      };

      const handleEnter = (e) => {
        if (e.key === "Enter") {
          e.preventDefault();
          addToArrayHandler();
        }
      };

      const handleSubmit = (e) => {
        e.preventDefault();
        const docRef = doc(db, "books", body.id);
        await updateDoc(docRef, {
          ...body,
          publish_date: Timestamp.fromDate(new Date(body.publish_date)),
        });
      };

      if(!body){
        return <p>"loading..."</p>
      }

      return (
        <div className="edit_container">
          <h3 className="edit_title">Edit Book</h3>
          <form onSubmit={handleSubmit} className="edit_form">
            <label>
              Title:
              <input 
                type="text" 
                value={body.title} 
                onChange={(e) => {
                  setBody({ ...body, title: e.target.value });
                }}
              />
            </label>
            <label>
              Author:
              <input 
                type="text" 
                value={body.author} 
                onChange={(e) => {
                  setBody({ ...body, author: e.target.value });
                }}
              />
            </label>
            <label>
              Date:
              <input
                type="date"
                value={body.publish_date}
                onChange={(e) => {
                  setBody({ ...body, publish_date: e.target.value });
                }}
              />
            </label>
            <label>
              Add a Character:
              <span className="add_character_container">
                <input
                  type="text"
                  value={character}
                  onKeyPress={handleEnter}
                  onChange={(e) => setCharacter(e.target.value)}
                />
                <button type="button" onClick={addToArrayHandler}>
                  Add
                </button>
              </span>
            </label>
            Character List:
            <ol className="character_list_container">
              {body.characters.map((item, index) => (
                <li key={index} className="character_item">
                  {item}
                  <button
                    type="button"
                    onClick={() => deleteFromArrayHandler(item)}
                    className="remove_character_btn"
                  >
                    X
                  </button>
                </li>
              ))}
            </ol>
            <button type="submit">Submit</button>
          </form>
        </div>
      );
    };

    export default Edit;    
    ```



Awesome, we just saw a great example on how to ***U***pdate data inside a Firestore DB. As mentioned before, there are several ways to update data, and though this is just one example, [feel free to explore other methods](https://firebase.google.com/docs/firestore/manage-data/add-data#:~:text=is%20more%20convenient.-,Update%20a%20document,-To%20update%20some) used to update data and make sure to use the methods that best fit your database. At the end of the day, consistency will be a crucial factor in your Firestore DB.

## Summary

Alright! We have covered all four basic operations that make up a **CRUD** app, that's: ***C***reate, ***R***ead, ***U***pdate, and ***D***elete. These four basic operations will help you create your first Full-Stack application with Firebase.  

## Additional Resources

- [ ] [YT, The Net Ninja - Getting Started with Firebase 9 #10 - Updating Documents](https://www.youtube.com/watch?v=Przhgs-GJ2s)
- [ ] [YT, The Net Ninja - Getting Started with Firebase 9 #5 - Adding & Deleting Documents](https://www.youtube.com/watch?v=s1frrNxq4js&list=PL4cUxeGkcC9jERUGvbudErNCeSZHWUVlb&index=5)
- [ ] [Blog, Soft Author - Raja Tamil - Firebase V9 Firestore DELETE Document Using deleteDoc()](https://softauthor.com/firebase-firestore-delete-document-deletedoc/)
- [ ] [Blog, Soft Author - Raja Tamil - Firebase V9 Firestore DELETE Document Using deleteDoc()](https://softauthor.com/firebase-firestore-get-document-by-id/)
- [ ] [Firebase 9 Firestore Get A Document By ID Using getDoc()](https://softauthor.com/firebase-firestore-update-document-data-updatedoc/)

## Know Your Docs

- [ ] [Firebase Documentation - Delete data from Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/delete-data)
- [ ] [Firebase Documentation - Add data to Cloud Firestore](https://firebase.google.com/docs/firestore/manage-data/add-data)
- [ ] [Firebase Documentation - firebase.firestore.Timestamp](https://firebase.google.com/docs/reference/js/v8/firebase.firestore.Timestamp)
- [ ] [Firebase Documentation - firebase.firestore.Timestamp](https://firebase.google.com/docs/reference/node/firebase.firestore.DocumentReference)
