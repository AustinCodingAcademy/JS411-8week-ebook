# Intro to Authentication

_Nothing will ever be attempted if all possible objections must first be overcome._

_—Samuel Johnson_

## Overview

Authentication is an important part of creating APIs. As I am sure we can all guess, authentication is used to lock down specific endpoints so that they cannot be freely accessed. To learn how to implement authentication, we will need to understand the process or **workflow** as well as a few new terms.

Although we will be building our server on [Google Firebase](https://firebase.google.com/), it is important to understand the fundamentals of core authentication. There are many ways to implement authentication into an app, but we will be discussing one of the more commonly used methods, [JSON Web Token/JWT](https://jwt.io/introduction) authentication. This requires us to communicate with a server from the client-side by sending some authentication data, _username_ and _password_. If the _username_ and _password_ match, we then receive an authorization token from the server, in which we store into our cookies session. This token, which is stored in the cookies, will then be appended to any request made by the user who was just authorized to get data from the server.

Let's get started!

### Why Authenticate?

Authentication is used by a server to give permission to a user based on the credentials they have provided. Without implementing some type of authentication to a server, the server can be exposed to data that we otherwise did not want to expose. Also, it allows anyone the ability to send multiple requests to routes that have been built, and that can lead to many problems such as database storage capacity exceeding certain limits, and storing data is not cheap. There is a lot of malicious intent surrounding cyber security, so making sure we set up some layer of protection is a must. It's important to understand authentication because it's necessary for the security of your app and it gives you some insight on what every app on the internet does when you sign in.

### Authentication vs Authorization

Let's first clear up the definition of these two words. Authentication is the process of verifying whether a person-user has access to a server; _Are they a user?_ It's like buying a ticket to a concert and flashing it at the gate(authentication), then you get a wristband(authorization) and you're allowed to go in and enjoy the music!

> ... but what's a _backstage pass_?
>
> - **Wristband** : Allows a person only access to the floor<br>
> - **Backstage** Pass : Allows a person access to both backstage area and the floor <br>
> - **Security Badge** : Allows a person to access any area and might has additional security access <br>
> - **The Band** : All-access (non-security), free drinks, and good times!
>
> Imagine these are Roles assigned to people at a concert, and although restrictions should apply to everyone, there is always someone trying to get in for free or trying to bypass the security.

When we build apps with data that needs to be allowed to certain person-users but restricted to others, we need to implement Authorization. This is the process of assigning roles to each person-user.

Maybe you're building a classroom management app for you and your students. All of the data for this app will be stored in the same database and served by the same server but you don't want your students to have access to other students' grades and turned-in assignments but still have access to their own assignments and grades. However, for you, as the teacher you want to be able to see all of the student's grades. To solve this problem you would assign each user of the app a role when they sign-up so each has specific levels of authorization. Teachers would get a `teacher` role, students would get a `student` role and maybe parents would get a `parent` role.

In an Express server you'd add an `if` statement to each route that asks if they are a teacher to access the resources behind the `getAllGrades()` so that `student` and `parent` users would be blocked from this particular resource.

In your Firebase project, you will be writing similar rules that may allow access using `if` statements asking if the current signed in user has a certain role.

For example, if a teacher/user is signed in, and that teacher is trying to access all data pertaining to grades for their students, that teacher/user must have the role `teacher` in order to access any documents about the students grades. This will prevent the roles `student` and `parent` from seeing these particular documents, unless those particular grades refer back to the student in particular. We can also set rules based on a user's id. This will allow us to connect certain documents with the current user that is signed in. So if a user/student is logged in, they should only have access to their grades and will be restricted from trying to see any other type of document stored in our database.

## The Steps of Authentication

Authentication is the process of comparing passwords to passwords to verify or authenticate the identity of a user.

![PIC](../images/stepsOfAuth.png)

1. The username and password are sent to the server.
2. The server accesses its database of users that holds the username and password.
3. The server checks the provided username & password against the username & password in the database.
4. If the credentials match, the user's identity is verified, and the application decides what's next.
5. If not, a generic error message is returned.

### The Sign-Up Overview

There's a difference between Sign-Up and Sign-In. We first need to Sign-Up, obviously.

![PIC](../images/writeToDatabase.png)

The first step of authentication is to sign up! After all, we can't verify your identity if we don't have credentials to compare with what you provide to confirm you are who you say you are.... When one signs-up on any web app, their credentials (username/email & password) will be sent from the front-end to the server and written to the database.

> NOTE: It's important to understand this because it will help you visualize how the server will be checking incoming "sign-in" credentials against previously written "sign-up" credentials.

1. Input and submit email/username & password info on front-end to "sign-up"
1. Front-End sends POST request with the the email/username & password to the server
1. The server receives the credentials and INSERTs a new entry in the users table
1. The user returns to the app to login by inputting and submitting their email & password on the front-end
1. The front-end sends a POST Request with the credentials to the server
1. The server SELECTS the previously written email that matches and checks to see if the passwords match
1. If true the next page in the app is sent to the front-end and a bearer token is stored in cookies (more on this soon)
1. If false another "login" page is sent to the front-end

### Hashing

There's a small step in the summary above that was excluded called `hashing`. See, when we store passwords in our database we don't want to store `plaintext` because if our database is ever breached(hacked) the passwords will be readable by human-eyes and simple javascript functions. To protect our users we create new strings that represent the passwords called a `hash`.

A `hash` is a unique and complicated string created by passing a simple string into a mathematical formula (algorithm) that scrambles and generates a unique string. The way it works is highly mathematical (luckily there are [Node packages](https://www.npmjs.com/package/argon2) for it) but in short it could look like this:

| Simple String | The Hashed String                |
| ------------- | -------------------------------- |
| pony          | 4B3E3C2F99046F92A61BAB6775848577 |
| apple         | 1F3870BE274F6C49B3E31A0C6728957F |
| pony          | 4B3E3C2F99046F92A61BAB6775848577 |

No matter what, if you pass `pony` through the hashing algorithm is will also produce the `4B3E3C2F99046F92A61BAB6775848577` every time. This is how passwords can be stored as hashes and later compared, hash to hash. We just use a hashing algorithm in the route on our server between receiving the request to "login" and when the server reads the previously stored hash in the database created during "sign-up".

> You can play with how the [MD5 hashing algorithm](https://passwordsgenerator.net/md5-hash-generator/) will create unique strings with any common string you put in here.

Once the plaintext password has been hashed the new unique String will be stored in the database along with the username/email.

##### The Code for Hashing

Below is a small Express server that has a hashing algorithm added to it called argon2. Read over the code and see if you can make sense of what's going on.

=== "Express App with Argon2 Hashing"

```javascript
const express = require("express");
// import argon for hashing
const argon2i = require("argon2-ffi").argon2i;
const crypto = require("crypto");
const bodyParser = require("body-parser");

// create express app
const app = express();
const jsonParser = bodyParser.json();

// post request route for when a user signs up for the app
app.post("/signup", jsonParser, function (req, res) {
  // if no data has been sent, send back status 400
  if (!req.body) return res.sendStatus(400);
  // using argon2, hash the request body that has the password.
  crypto.randonBytes(32, function (err, salt) {
    if (err) throw err;
    argon2i.hash(req.body.password, salt).then((hash) => {
      // don't log in production code...for learning purposes only
      console.log(hash); //...replace with code to write the username & password to the database

      // then send a 201 status that it was successful.
      res.sendStatus(201);
    });
  });
});

// ...more routes would go here...

app.listen(3001, function () {
  console.log("listening on port 3001");
});
```

As you might have seen, when someone sends a `POST` request to the `/signup` route, it should include a `username` and `password`. If it does, the server will run the hashing function `crypto.randonBytes` & `argon2i`.hash on the password. You are probably wondering what `salt` is. `Salt` is the number of times the algorithm is supposed to run before the hash is determined "complete".

Hackers have access to run the same algorithm that creates your password hashes. This means, if they get ahold of your list of usernames & passwords they can run them backwards as well and learn the plaintext version of your passwords and then access your user's data. Nevertheless, they will still be guessing at possible inputs to get to the correct password. To break through this barrier they will formulate something called a Brute Force attack, where in, they tell a powerful computer to run the same algorithm over and over on the list of hashed passwords attempting to get the right passwords. This is where a salt round comes in. A salt round is the number of times the algorithm scrambles the plaintext password. 1 salt = 1 time, 5 salts = 5 times. Each time you increase the salt you increase the difficulty for the hacker by a factor of about 10! By increasing this number you make it more expensive in both time and energy for the hacker to make it profitable to hack your users. The double-edge of this sword is that it also makes it more expensive for your computers to run the hashing algorithm. The trick is to find a happy medium! Usually 12 is the ideal number; but, some have suggested [you calculate the number with the total amount of time you can stand](https://security.stackexchange.com/questions/17207/recommended-of-rounds-for-bcrypt).

To get an idea of why salting is so important when hashing password, check out this post from 2011.

![PIC](../images/securityStackExchange-saltingGuesses.png)

### The Sign-In Overview

Now that we know passwords will be hashed on `sign-up`, what happens when a user signs-in?

Obviously we don't want our user to have to input a username and password for every page and resource they'd like to access. Instead, we want them to have them sign-in once and then allow them to freely move around their account until they sign-off.

The trouble is that our server (just a computer) doesn't know who they are like we humans would if we saw them. So, to make this work we have to give the user a "wristband" that they would show to each part of the server when they wanted to see a new page or resource. This "wristband" is called a bearer token.

A `bearer token`, or a `JSON Web Token/JWT`, is a unique set of letters and numbers created by the server the represents a successful sign-in. Its generated when username & passwords match and sent back to the client (the user) and stored on their device so that it can be sent back to the server with each new subsequent request to see a new page or resource. In this way, the user can move freely about their account without worrying about signing-in over and over; but instead we developers just have to be smart enough to make that front-end client send the bearer token back with each new request, and make our server require a bearer token to allow the resources to be sent back with the response.

### Creating a JWT

**A JWT might look like this:**

```console
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

Look closely and you'll see two `"."` periods between these random strings of letters and numbers. These separate the token into three parts:

| Part Name | Example                                                                    | Definition                                                                                                   |
| --------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Header    | eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9                                       | includes information about the type, as in JWT, and the algorithm, alg, used to created it.                  |
| Payload   | eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ | the actual data stored in it, like the username & iat (issued at) which tells the time the token was issued. |
| Signature | SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c                                | contains the hash of our server's key                                                                        |

## Authentication Workflow

Now let's talk through the process from a high perspective. You'll be seeing code snippets as we go but just know there may be some modifications to this code in live code bases. But please read the pseudo-code so you picture, for yourself, this process.

The first step in this process is that the client/front-end will make a request to a server/API:

```javascript
// front-end
axios.get("https://ourapi.com/user?ID=12345").then(function (response) {
  // handle success
  console.log(response);
});
```

Just as a server is built to do, it will be listening for `requests` to that URL endpoint and return a `response` with the resource that was requested:

```javascript
// back-end
app.get("/users", (req, res) => {
  // perform some logic to go get data from database
  res.json(users);
});
```

But now we want to see if the user is registered in our server, aka `authenticate` them, before we let them get to the resource they want... To do this the server will ask the user to sign-in with their username and password. If they are successful with their sign-in, the server will send to them a "wristband", or an `authorization token`, that proves they have been `authenticated`. Now that they have been `authorized`, the stored `token` will be used on all of their following requests (until they logout) so they don't have to keep entering their username and password. This token is called a `bearer token`.

```javascript
// back-end
const login = (req, res) => {
  const { username, password } = req.body

  // * build and call your own authentication function using our server's secret key
  const jwtSecret = 'secret123'

  app.get('/jwt', (req, res) => {
    const token = jsonwebtoken.sign({ user: 'username' }, jwtSecret)

    // the response object has a method on it called` that takes three arguments:
      // * name of the cookie
      // * value of the cookie
      // * parameters of the cookie
    // and sets a cookie on the user's browser/client.
    res.cookie('our_token', token, {httpOnly: true})

    res.json({ token })
  });

  // -or-

  // * send the username & password to a third-party like Auth0, see below:
  axios(`https://${process.env.AUTH0_DOMAIN}/oauth/token`, {
    // ...more on this later...
  })
  .then(response => {
    // if the username & passwords are correct send the token back to the client/front-end
    const token = response.data.access_token
    res.cookie('our_token', token, {httpOnly: true})

    res.json({ token })
  })
  .catch(e => {
    res.send(e)
})
```

Once the `res.cookie` method has been called a cookie that is specific to our server's domain has been set on the user's browser/client and it's sent in the headers of each subsequent request:

```javascript
// front-end

// create a configuration object with the the correct keys and values
// the token should be in the headers
const config = {
  withCredentials: true,
  headers: { Authorization: `Bearer: ${document.cookies.our_token}` },
};

// send the config object with the request
axios("https://ourapi.com/user?ID=12345", { config }).then(function (response) {
  // handle success
  console.log(response);
});
```

### Reading the JWT

Now we'll build some logic into our server that asks to see that token _"wristband"_ and verifies if it's valid before sending the requested resources back.

```javascript
// back-end
const checkForAuthToken = (req, res, next) => {
  const specialToken = req.headers["our_token"];

  if (!checkIsValid(specialToken)) return res.sendStatus(401);
  next();
};

// build your own
const checkIsValid = (token) => {
  // this function would run the RFC 7519 algorithm to see if the token is valid(see below)
  // * if valid return true
  // * if not valid return false
};

//  -- or --
// use a third-party like Auth0
```

If this check fails we could choose to send them a 403 or re-route them to the login page, ...or both!

### But Why?

This is a good question! Why do we need to a JWT with a header, payload and signature? The answer to this question is security.

Think way back to when we first learned about HTTP(S) and how the internet is possible because computers are all built to read the same language and use the same protocol(HTTP). This means that all information sent over wifi, fiber, coax, satellite or copper is available to all computers in-between you and the server you're talking to across the country.

This space between you and that server or other computer is a very vulnerable space because it can be intercepted and read by many computers without you evening knowing. For this reason we have to `encrypt` the data we need to be private. `Encryption` is the act of "scrambling" the information in a mathematical way with a key only the sender and the receiver have. ...And this is the foundation of Cyber Security.

With this in mind you might be thinking that creating your password hashes and bearer tokens is very difficult. It's actually not because we just use Node packages to generate them and we just tie them together to make them work for our app.

<!-- (https://www.youtube.com/watch?v=7Q17ubqLfaM -->

## Additional Resources

- [ ] [YT, Web Dev Simplified - JWT Authentication Tutorial - Node.js](https://www.youtube.com/watch?v=mbsmsi7l3r4)
- [ ] [YT, Fireship - Session vs Token Authentication in 100 Seconds](https://www.youtube.com/watch?v=UBUNrFtufWo)
- [ ] [YT, Ben Awad - How to Store JWT for Authentication](https://www.youtube.com/watch?v=iD49_NIQ-R4)
- [ ] [Article, Tania Rascia - Client-side Authentication the Right Way (Cookies vs. Local Storage)](https://www.taniarascia.com/full-stack-cookies-localstorage-react-express/)
- [ ] [Article, OWASP - Cookie & CSRF, Cross-Site Request Forgery](https://owasp.org/www-community/attacks/csrf)
- [ ] [Article, Veracode - Zero to Hashing in 10 minutes](https://www.veracode.com/blog/secure-development/zero-hashing-under-10-minutes-argon2-nodejs)
- [ ] [Article, jwt.io - Introduction to JSON Web Tokens](https://jwt.io/introduction)

## Know Your Docs

- [ ] [NPM Docs - argon2](https://www.npmjs.com/package/argon2)
- [ ] [NPM Docs - jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)
- [ ] [MDN Docs - Web Authentication](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API)
