# Intro to CRUD - Create, Read, Update, Delete
_Nothing contributes so much to tranquilize the mind as a steady purpose—a point on which the soul may fix its intellectual eye. —Mary Shelley_

<!-- TODO, I'm not really sure this Intro to CRUD works with the Firestore walk through but maybe it does. I'm going to leave it for now, Clayton 7.1.22 -->

## Overview

For the past couple of days, we have been learning a lot about **Firebase Authentication** services specifically, to store authenticated users on the cloud somewhere. These next couple of lessons will introduce a new service from **Firebase** called [**Firestore**](https://firebase.google.com/docs/firestore) which will allow us to store data like products, businesses, or whatever your Capstone app may need to a database. This data will be stored as records called **collections**, and these **"collections"** will have several more records within each collection called **documents**. We will be creating a client side **UI** which will enable us to make queries to this database of `collections` to not only read these documents, but display it to the user as well. We will also be implementing a way to to **create**, *update*, or *delete* these *documents* or *collections* on our Database.

But, before we get into **Firestore**, we want to talk about fundamentals of **Database Management Systems** and the basic operations we use to obtain and **mutate**/_change_ data called **CRUD**. By the end of your course and by graduation you will have built a full-stack CRUD app so let's get to learning about what these guys are.

## What's CRUD?

**CRUD** is an acronym that stands for **C**reate, **R**ead, **U**pdate, and **D**elete. In its simplest forms, any Software Application that consists of these four basic operations can be considered a `CRUD` application.

* **C** stands for the **creation** of data or the entry of a new piece of data like when you want to create a new user or product.

* **R** stands for the **reading** of the data. Think when you want to show a feed you'll need to make a read request to read the data in the database to show on the screen for the user. 

* **U** stands for **updating** the data like when you need to change the price of a product in your database or when you need to add a comment to a post. You're updating the data.

* **D** stands for **deleting** data. This is straight-forward because it's just removing the data from the database.

At a higher level, CRUD apps consist of three major parts: the **database**, **UI**(_user interface_)/front-end, and the server(*API*)/back-end.

### What is a Database

Almost everything we do on the internet, from the pictures we view, blogs and all the Wikipedia pages we read, all store their information somewhere. These bits of information have to be stored somewhere, that's where databases come into play. A **Database** helps us store and organize our data, enabling us to easily read, create, update, and delete that data. The database is where our **Data** will be stored.

A **DBMS/_Database Management System_** is a service in which we use to **create** and **manage** our database. We will be using **Firebase's Firestore** as our **DBMS**, but there are also [several other services in which we can host our Database](https://www.softwaretestinghelp.com/database-management-software/).

There are also several types of **Database Management Systems** that can be categorized in the way in which they store data. The more popular types include **_Relational Databases_** **(SQL)** and **_Document Stores_** **(NoSQL)**. As you may have already guessed, Firestore is a **NoSQL DBMS** which means it isn't relational like SQL but instead is a collection of documents.

We will spare you the details about every database service available, but if you are interested in learning more,  check out this [intro to databases and styles guide](https://budibase.com/blog/best-database-management-software/).

### The UI / _User Interface_

The **_UI_** or _user-interface_ will include everything we have learned about building applications in React so far as a way for users to interact with our database. Let's say, for example, we have an app that stores a _collection_ of a users favorite games or books. When that user signs up, we want our App to direct the user to their Dashboard and maybe render that specific user's current list of favorite games. The user themselves aren't making the request, that request is programmed to happen when that user signs-in. When it comes to creating or updating data, the user will usually interact with a _form_ (`onSubmit`) and _buttons_ (`onClick`) that interact with the database based on those events. We will program or application to handle these events and make them interact with our **_DB_** accordingly. We can also provide a search bar for the user to make special queries to our database that filters specific data the user is looking for. We will learn more about how to do that with Firestore as we progress through the course.

### The Server or API

APIs are how most developers create full-stack web applications. Usually, this is an application separate from our client-side which allows us to make special **HTTP requests** to our database, also known as a _server-side application_. These special requests are handled by something known as **routes**, and they will be responsible for what actions need to be performed when called. For instance, a **GET** request gets, or reads, data; while a **POST** requests posts, or creates data. These two requests would be handled by two different routes, aka **Request Handlers**.

These **route** functions may vary depending on the needs of the app, but they are usually designed to carry out the four basic CRUD operations: Create, Read, Update, and Delete. Web applications that separate client and server side are considered [**REST APIs**](https://www.codecademy.com/article/what-is-rest), "_**RE**presentational **S**tate **T**ransfer_". We do not need to go deep into details for this, but just know this is a very common practice.

While creating server-side apps have become increasingly easier, we will not need to create a separate server since Firebase provides us with a database(store) and a server with authentication. We'll be using the [Firestores _Software Development Kit_ / **SDK**](https://firebase.google.com/docs/firestore/client/libraries) to build the server, combined with [Firestore Security Rules](https://cloud.google.com/firestore/docs/security/get-started) for authorization and [Firebase Auth](https://firebase.google.com/docs/auth/) services to authenticate users.


## Additional Resources

- [ ] [YT, Your IT Class - REST Vs CRUD - Explained with usecase in 5 Minutes](https://www.youtube.com/watch?v=Pz1IcBjOxj8)
- [ ] [Blog, budibase - What is a CRUD app and how to build one | Ultimate guide](https://budibase.com/blog/crud-app/)
- [ ] [Blog, budibase - 14 Best Database Management Software to use in 2021](https://javascript.plainenglish.io/what-is-double-bang-operator-in-javascript-90fc67ead5a4)
- [ ] [Article, codecademy.com - What is REST?](https://www.codecademy.com/article/what-is-rest)