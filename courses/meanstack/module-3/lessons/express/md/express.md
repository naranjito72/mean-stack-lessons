# Express

### Web Frameworks

**Why would I use a *framework*?**

[Web Frameworks](https://en.wikipedia.org/wiki/Web_framework) or web application framework (WAF) is a software framework that is designed to support the development of web applications including web services, web resources and web APIs. Web frameworks aim to alleviate the overhead associated with common activities performed in web development.

For example, many web frameworks provide:
- Libraries for database access
- Templating frameworks
- Session management
- Often promote code reuse

Though they often target development of dynamic websites they are also applicable to static websites.

We can build a full-blown web application using just Node.js, Ruby, Python or any other backend language. Over time though, people have developed *frameworks* on top of these different languauges for a few reasons:

- We do many of the aforementioned tasks for *every* web application, and it's tedious to set up.
- We need a way to structure our code, all of our complex logic can build up over time, leaving us with a mess.
- We benefit from other people's hard work. If you're using your own framework, then every bug is yours to fix. With a community surrounding the framework, we get some help in this regard.

## Express Web Framework

![](https://i.imgur.com/T9ARM9m.png)


[ExpressJS](http://expressjs.com/) is the most commonly used framework in the Node.js ecosystem. Every Node.js player has heard of it and is using it with or without noticing.

It’s currently on its 4th generation, and there are quite a few [Node.js frameworks](http://expressjs.com/en/resources/frameworks.html) built based upon it or inspired by its concepts.

Express.js, or simply Express, is a web application framework for Node.js, released as free and open-source software under the MIT License.

It is designed for building web applications and APIs. It is the de facto standard server framework for Node.js. The original author described it as a relatively minimal with many features available as plugins.

Express is the backend part of the MEAN stack, together with MongoDB database and AngularJS frontend framework.

Ready to Start?

### Express Hello World

[ExpressJS](http://expressjs.com/) is a web framework built on Node.js that has functions that closely resemble the request-response process.

Let's get set up with our first Express app.

**1 |** Create a folder called `express-hello-world`.

```shell
$ mkdir express-hello-world
$ cd express-hello-world
```

**2 |** Install **Express** with NPM and save it as a dependency in our project, then create a file to run our *server* named `app.js`

```shell
$ npm init
(Hit return until prompted to type "yes")

$ npm install express --save
$ touch app.js
```

**3 |** Write our `app.js` server

We have to first require Express so we can use it in our app.

The [Express()](https://expressjs.com/en/4x/api.html#express) constructor instantiates an [express application](https://expressjs.com/en/4x/api.html#app).

```javascript=
const express = require('express');

// We create our own server named app
// Express server handling requests and responses
const app = express();
```

**4 |** Set up a Route

Web Apps have many different pages, and we need to tell our server what to do when it receives a request. Normally a server identify requests with two parameters:

- **URLs**
  What goes after the http://domain.com/****

  - `/profile` for example.com/profile
  - `/blogs`  for example.com/blogs
  - `/` for example.com

- **HTTP Method**: `get`

```javascript=
const express = require('express');
const app = express();

// our first Route
app.get('/', (request, response, next) => {
  console.log(request);
  response.send('<p>Welcome Ironhacker. :)</p>');
});
```

Notice, each route will accept a *callback*. This is the function that will be called when someone makes a request to `/`.

- **app**: Our express server
- **`get`**: the **HTTP Verb** needed to access this page
- **`/`**: the route that the User will type into the URL bar
- `request`: An *object* containing information about the request, such as the headers. More on this later
- `response`: An *object* containing information about the response, such as headers and any data we need to send to the client

The two parameters of the `request` and the `response` will always be passed to the callback function for any route.


**5 |** Start the Server!

Tell our server to *continuously listen for requests* on port 3000:

```javascript
// Server Started
app.listen(3000, () => {
  console.log('My first app listening on port 3000!')
});
```

**Final Product**

```javascript=
// Require Express
const express = require('express');

// Express server handling requests and responses
const app = express();

// our first Route:
app.get('/', (request, response, next) => {
  response.send('<p>Welcome Ironhacker. :)</p>');
  next();
});

// Server Started
app.listen(3000, () => {
  console.log('My first app listening on port 3000!');
});
```

To view your first web app, we must run the server with node. Remember that because we executed `app.listen()`, the program will run until we stop it manually.

```
$ node app.js
```

And visit [localhost:3000](http://localhost:3000)!

:::info
:bulb: To stop the server, type `CONTROL`+`C` in the terminal
:::

## Static Files

Static files are things like images, CSS, and client-side JavaScript that are sent directly from the server to the browser as is.

Express has built in support for serving these kinds of files.

Typically, these files are saved in a folder called `public`:

```
$ mkdir public
```

Let's create a folder for images, and download a cool cat picture to that folder:

```
$ cd public
$ mkdir images
$ cd images
$ curl -o cool-cat.jpg http://wallpapercave.com/wp/X7VjxFk.jpg
```

Inside of Express, we have to tell our server to serve static files from the `public` directory:

```javascript
// ...
const app = express();

app.use(express.static('public'));

app.get('/', (request, response, next) => {
// ...
```

Visit [localhost:3000/images/cool-cat.jpg](http://localhost:3000/images/cool-cat.jpg) and you will see your image!

We aren't going to have a web app full of static files, where people have to visit a million different pages to see different pictures.

One of the benefits of using static assets is that we can incorporate them into our HTML for the browser to read.

**Create a stylesheet:**

```
$ mkdir public/stylesheets
$ touch public/stylesheets/style.css
```
**Add the following styles:**

```css
body {
  color: blue;
  background-color: bisque;
}
```

**Create a new route:**
```javascript
// ...

app.get('/hello', (request, response, next) => {
  response.send(`
    <!doctype html>
    <html>
      <head>
        <link rel="stylesheet" href="stylesheets/style.css">
      </head>
      <body>
        This is my second route
      </body>
    </html>
  `);
});

// ...
```

Now visit [localhost:3000/hello](http://localhost:3000/hello)!

:::danger
:warning: Remember to restart your server in your terminal before checking the changes.
```
$ ctrl + c
$ node app.js
```
:::



### Statics Assets Request-Response Flow

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_e9728aae585f81940c61289c0125f9f2.png)


## Summary

In this lesson we discussed why and how we would use a web application, and how to build a *super* basic web app with Express. We also discussed the building blocks of the internet, HTTP.

HTTP and web concepts are almost a language on their own. We're going to continue to reinforce and use the terms `request`, `response`, and many more going forward.

## Extra Resources

- [Express Getting Started](https://expressjs.com/en/starter/installing.html)
- [Express Hello World](https://expressjs.com/en/starter/hello-world.html)
- [What is HTTP(video)](https://www.youtube.com/watch?v=eesqK59rhGA)
- [HTTP Made Really Easy](https://www.jmarshall.com/easy/http/)
- [A Beginner’s Guide to HTTP and REST](https://code.tutsplus.com/tutorials/a-beginners-guide-to-http-and-rest--net-16340)

![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# Express | Middleware: Nodemon, Morgan, and Node debug

## Learning Goals

After this lesson you will be able to:

- Understand and use the middleware pattern in Node
- Keep your server running and restart the server if you make changes
- Log information with Morgan
- Debug more efficiently with Node Debug

## Introduction

Before this point, we've been referencing the mysterious `app.use()` function. The function is aptly named, and we can assume we're telling our application to use a specific package, but let's take a deeper look into how this process works.

## Middleware

When a request is made to our Express server, it doesn't actually go straight to the route. Often times, our route is actually the last stop.

We've used a couple of packages thusfar, including bodyParser. These packages are called *Middleware*.

>The term middleware is used to describe separate products that serve as the glue between two applications.
>
>Middleware is sometimes called plumbing because it connects two sides of an application and passes data between them.

In this case, the two sides of the application consist of (1) the client making a request, and (2) the server handling that request.

The following diagram illustrates how our application actually handles a request.

![Express App Requests](https://i.imgur.com/AO6lw3m.png)

1. The request passes through `cookieParser`
2. The request passes through `bodyParser`
3. The request passes through `logger`
4. The request passes through `authentication`
5. Finally, our request actually hits our route, and callback for it

How does this work? Let's create a simple example to illustrate this.

First, let's create a test route:

```javascript
app.get('/test', (req, res) => {
  res.send("We made it to test!");
});
```

Then, let's create a middleware of our own:

```javascript
// ...
app.use(myFakeMiddleware)
// ...
function myFakeMiddleware(){
  console.log("myFakeMiddleware was called!");
}
```

Make a request to `localhost:3000/test`:

![](https://i.imgur.com/Lnqfi8P.png)

But our browser doesn't load anything! Why?

### Middleware Pattern

`app.use()` is a function that adds a middleware to our stack. All of the middlewares are called, one after the other, finally ending with your route.

The problem is that we're not calling our next middleware. The chain is broken, and there is a clog in the pipe.

Functions that work as middlewares receive 2-4 arguments and one of them is always the *next* middleware to call.

Let's add that to our function:

```javascript
function myFakeMiddleware(_, _, next){
  console.log("myFakeMiddleware was called!");
  next();
}
```

:::info
:bulb: We'll discuss the first two arguments shortly!
:::

We pass `next` as our third argument, then whenever our middleware is done logging, we call it.

Visit `localhost:3000/test`.

#### Passing Information

Unless we're simply logging the request, often times we will need to pass information through our middleware.

Express suggests attaching any of your data to the `request` object. This will then be available in every middleware, and in your route. Let's take a look at this example of a fake middleware:

```javascript
function myFakeMiddleware(req, _, next){
  console.log("myFakeMiddleware was called!");
  req.secretValue = "swordfish";
  next();
}
```

After our `myFakeMiddleware` middleware is called, we can easily access the *modified request* object. In this example, we can access `secretValue`:

```javascript
app.get('/test', (req, res) => {
  let mySecret = req.secretValue;
  res.send(mySecret);
});
```

Often times we won't be designing a middleware of our own, Express already has a [huge ecosystem of middlewares](https://expressjs.com/en/resources/middleware.html), but it is quite helpful to understand how the request is processed.

Let's talk about some extremely useful Node packages (some of which are middlewares) that will help you when developing apps.

## Nodemon

I'm sure you've noticed that every time we make a change in our Express application, we have to kill the server and start it again. Maybe you've forgotten to restart after making a change and don't know why your code isn't working. Quite a pain.

![nodemon logo](http://i.imgur.com/QHkm6Ct.png =350x)

[*Nodemon*](https://github.com/remy/nodemon) is a Node.js app reloader. In short, it will watch for any file change, and then restart your application when something is different. It is a [CLI](https://en.wikipedia.org/wiki/Command-line_interface) application that can be installed through npm:

```
$ npm install -g nodemon
```

Nodemon is meant to be a drop in replacement for the `node` command. We can fire up our Express server with reloading by running the following:

```
$ nodemon app.js
```

And that's it! We can stop our server as we normally would with `ctrl-c`. There are plenty of advanced options that we shouldn't worry about currently [in the docs](https://github.com/remy/nodemon).

## Morgan

Imagine this scenario.

After you graduate Ironhack, you go and get yourself a fancy new developer job. You're the only developer on a new startup creating the Tinder for people who like JavaScript, and you get a call at 3AM in the morning from the CEO: "Ironhacker, the server is down! Everything is broken!" What do you do?

In the current state of our application, you would be doing a lot of guessing. Possibly trying to visit every route to see which one is broken, guessing what the problem is, and generally having a bad time.

Enter *Logging*

![wrong logging ](https://i.imgur.com/kNQscIy.jpg)

No, not *that* kind of logging, like this:

![A log file screenshot](https://i.imgur.com/CsAkpjg.png)


> Logging is the process of recording application actions and state to a secondary interface.

The logger may log information about the request, such as:

- The HTTP method
- URL that was requested
- The time and date a request occurred
- The request headers
- The origin of the request

This makes it way easier to find out why your server is on fire, and makes it much easier to troubleshoot in development.

Enter [Morgan](https://github.com/expressjs/morgan). Morgan is a flexible, configurable, npm middleware that handles logging for us. First, let's install Morgan:

```
$ npm install --save morgan
```

And then require it in our express app:

```javascript
/* other require statements */
const morgan     = require('morgan');
```

Finally, we have to add Morgan to our middleware stack:

```javascript
/* other code */
app.use(
  morgan(`Request Method: :method, Request URL: :url, Response Time: :response-time(ms)`));
```
What is this sorcery? In short, we can pass symbols representing specific parts of the request into our Morgan function, it will read these, and then log that information when a request is made.

Right now, we're logging `:method`, `:url`, and `:response-time`.

Make a request to your home page, and then look in your terminal:

```
Request Method: GET, Request URL: /, Response Time: 560.786(ms)
```

This format makes Morgan super easy to configure. You can make the logs as large or as small as you need to, but Morgan has a few pre-built suggestions for you.

Let's change the middleware to Morgan's `dev` log level:

```
app.use(morgan('dev'));
```

Make another request to your home page:

```
  GET / 304 99.993 ms - -
```

The `dev` level logs the `:method`, `:url`, `:status`, `:response-time`, and `content-length`.

You can find all of the different logging *tokens* [in Morgan's documentation](https://github.com/expressjs/morgan#tokens).

## Node Inspector

Version 6.5+ of Node.js comes with a cool new experimental feature to debug your JavaScript code.

[Remember all of those cool debugging features](https://hackmd.io/OwVgjADJAsBmC0BmAnNM9ogIYngDhAGMA2eMAJgFMATEw884wiIA) that Chrome has? Node has taken advantage of these, and created a connection between your Node app and the Chrome developer tools.

To open these developer tools, we run our application with the `--inspect` flag.

```
$ nodemon --inspect app.js

Warning: This is an experimental feature and could change at any time.
To start debugging, open the following URL in Chrome:
    chrome-devtools://devtools/remote/serve_file/@62cd277117e6f8ec53e31b1be58290a6f7ab42ef/inspector.html?experiments=true&v8only=true&ws=localhost:9229/node
```

As discussed in the earlier lesson, we can add breakpoints and watchers.

Breakpoints will only be run when our code is run. In web development, this can be super handy for tracking a request, or catching a bug in our middleware.

In addition to this, if things get *really* tricky, we can browse our sources tab, and add a breakpoint to our included `node_modules` code.

Add a breakpoint to the `render` on your home page:

![](https://i.imgur.com/umtcbA4.png)

Now we can look at our request object, and see all of the information it has accumulated on its journey through the middleware:

![](https://i.imgur.com/jvNGcJ7.png)

If you need a refresher on the dev tools and debugging, feel free to revisit the previous lesson. The dev tools function almost exactly in the way that you think they would with Node.

## Summary

In this lesson we talked a bit about the middleware pattern. This is important to cover so you can understand what we're doing when we call `app.use()` and what all of these mystery packages are doing.

In addition we covered some important middleware packages such as Morgan, Nodemon, and the `--inspect` flag for Node.

Logging is *absolutely vital* to your application, and restarting your Node app every time you make a change is pretty frustrating, so these are going to become a very common part of your Node setup.

Debugging through the terminal and a series of `console.log` becomes very tedious as well, so try to use the `--inspect` flag as much as you can.

There are dozens of different middlewares for Node out there, so feel free to explore a bit more to see what they're capable of.

## Extra Resources

- [Debugging Express](https://expressjs.com/en/guide/debugging.html)

