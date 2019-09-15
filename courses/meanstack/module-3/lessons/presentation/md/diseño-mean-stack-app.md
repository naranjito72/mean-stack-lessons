# 1. Arquitectura Mean-stack

Empezaremos repasando el concepto convencional de la arquitectura MEAN. Después, mediante ejemplos, pasaremos a modificar algo las cosas. MEAN es una pila de desarrollo muy potente que permite resolver un aplio rango de problemas.

## 1.1. Arquitectura MEAN convencional

La manera común de trabajar con la pila MEAN es mediante una API REST que alimenta una SPA. La API se construye con MongoDB, Express, and Node.js, mientras que la SPA se hace en Angular. Esta aproximación es la manera más popular y eficiente para aquellos que vienen de Angular y buscan una API rápida y potente. Como se muestra en la siguiente figura:

![](https://imgur.com/wCzXbSo.png)

Figure 2.1 is a great setup, ideal if you have or intend to build an SPA as your userfacing side. Angular is designed with a focus on building SPAs, pulling in data from a REST API as well as pushing it back. MongoDB, Express, and Node.js are also extremely capable when it comes to building an API, using JSON all the way through the stack, including the database itself.
This is where many people start with the MEAN stack, looking for an answer to the question, “I’ve built an application in Angular; now where do I get the data?”

Having an architecture like this is great if you have an SPA, but what if you have differing requirements? The MEAN stack is far more flexible than the current design suggests. All four components are individually powerful and have a lot to offer. 

_What is a REST API?_
REST stands for REpresentational State Transfer, which is an architectural style rather than a strict protocol. REST is stateless; it has no idea of any current user state or history.
API is an abbreviation for application program interface, which enables applications to talk to one another. In the case of the web, an API is normally a set of URLs that respond with data when called in the correct manner with the correct information. A REST API is a stateless interface to your application. In the case of the MEAN stack, the REST API is used to create a stateless interface to your database, enabling a way for other applications, such as an Angular SPA, to work with the data. In other words, you create a collection of structured URLs that return specific data when called.

## 1.2. Más allá de SPA

En ciertas ocasiones tenemos requerimientos para los cuales la SPA no es la mejor alternativa. Vamos a repasar algunos de ellos:

### 1.2.1 Difícil de Indexar (crawling)

Las apps de JavaScript son difíciles de indexar. Los motores de búsqueda normalmente miran el contenido HTML de la página pero no ejecutan o descargan 
JavaScript. 
Tampoco funcionan bien las previsualizaciones automáticas de las redes sociales: Facebook, LinkedIn y Pinterest, ya que utilizan la información de HTML para extraer el texto y las imágenes relevantes.

Algunas maneras de resolver esto es:

__Un SPA crawlable__

Crear páginas HTML que reflejan el contenido del SPA. El servidor creará una versión HTML del sitio que se liberará a los _web crawlers_, o bien, utilizar navegadores sin cabeceras; `PhantomJS` , para correr la app JavaScript y utilizar el HTML resultante.

Cada método requiere un cierto esfuerzo de mantenimiento que suele crecer conforme los sitios webs se hacen más complejo.
Puede haber problemas de SEO si el HTML generado se diferencia bastante de la versión SPA. La web será penalizada. En el caso del navegador PhantomJS la salida puede ralentizar la velocidad de la página, lo que también es penalizado por el motor de Google.

__DOES IT MATTER?__

Whether this matters depends on what you want to build. If the main growth plan for whatever you’re building is through search engine traffic or social sharing, you want to give these concerns a great deal of thought. If you’re creating something small that will stay small, managing the workarounds is achievable, whereas at a larger scale, you’ll struggle.

On the other hand, if you’re building an application that doesn’t need much
SEO—or indeed, if you want your site to be harder to scrape—you don’t need to be concerned about this issue. It could even be an advantage.

### 2.2.2 Analytics and browser history

Analytics tools like Google Analytics rely heavily on entire new pages loading in the browser, initiated by a URL change. SPAs don’t work this way. There’s a reason why they’re called single-page applications!

After the first page load, all subsequent page and content changes are handled internally by the application. The browser never triggers a new page load; nothing gets added to the browser history; and your analytics package has no idea who’s doing what on your site.

__ADDING PAGE LOADS TO AN SPA__

You can add page load events to an SPA by using the HTML5 history API, which will help you integrate analytics. The difficulty comes in managing this and ensuring that everything is being tracked accurately, which involves checking for missing reports and double entries.

The good news is that you don’t have to build everything from the ground up. Several open source analytics integrations for Angular are available online, addressing most of the major analytics providers. You still have to integrate them into your application and make sure that everything is working correctly but you don’t have to do everything from scratch.

__IS IT A MAJOR PROBLEM?__

The extent to which this is a problem depends on your need for undeniably accurate analytics. If you want to monitor trends in visitor flows and actions, you’re probably going to find analytics easy to integrate. The more detail and definite accuracy you need, the more work it is to develop and test. Although it’s arguably much easier to include your analytics code on every page of a server-generated site, analytics integration isn’t likely to be the sole reason to choose a non-SPA route.

### 2.2.3 Speed of initial load

SPAs have a slower first page load than server-based applications, because the first load has to bring down the framework and the application code before rendering the required view as HTML in the browser. A server-based application only has to push out the required HTML to the browser, reducing latency and download time.

__SPEEDING THE PAGE LOAD__

You have some ways of speeding up the initial load of an SPA, such as a heavy
approach to caching and lazy-loading modules when you need them. But you’ll never get away from the fact that the SPA needs to download the framework (at least, some of the application code) and will most likely hit an API for data before displaying something in the browser.

__SHOULD YOU CARE ABOUT SPEED?__

The answer to whether you should care about the speed of the initial page load is, once again, “It depends.” It depends on what you’re building and how people are going to interact with it.
Think about Gmail. Gmail is an SPA and takes quite a while to load. Granted, this load time is normally only a couple of seconds, but everyone online is impatient these days and expects immediacy. But people don’t mind waiting for Gmail to load because it’s snappy and responsive once you’re in. And when you’re in, you often stay in for a while.
But if you have a blog pulling in traffic from search engines and other external links, you don’t want the first page load to take a few seconds. People will assume that your site is down or running slowly and will click the Back button before you’ve had the chance to show them content.

### 2.2.4 To SPA or not to SPA?

Just a reminder that the preceding sections aren’t an exercise in SPA-bashing; we’re just taking a moment to think about some things that often get pushed to the side until it’s too late. The three points about crawlability, analytics integration, and page load speed aren’t designed to give clear-cut definitions about when to create an SPA and when to do something else. They’re there to give a framework for consideration.

It may be the case that none of those things is an issue for your project and that an SPA is definitely the right way to go. If you find that each point makes you pause and think, and it looks as though you need to add workarounds for all three, an SPA probably isn’t the way to go.

If you’re somewhere in between, it’s a judgment call about what’s most important and, crucially, what’s the best solution for the project. As a rule of thumb, if your solution includes a load of workarounds at the outset, you probably need to rethink it.

Even if you decide that an SPA isn’t right for you, that doesn’t mean that you can’t use the MEAN stack. In the next section, we’ll take a look at how you can design a different architecture.

## 2.3 Designing a flexible MEAN architecture

Usamos MongoDB, Express y NodeJS para algo más que construir una API

A tener en cuenta:

- MongoDB can store and stream binary information.
- Node.js is particularly good for real-time connections using web sockets.
- Express is a web application framework with templating, routing, and session management built in.

What we can do here is give you a simple example and show you how you can fit
together the pieces of the MEAN stack to design the best solution.

### 2.3.1 Requirements for a blog engine

In this section, you’ll take a look at the familiar idea of a blog engine and see how you can best architect the MEAN stack to build one.

A blog engine typically has two sides: a public-facing side serving up articles to readers and (we hope) being syndicated and shared across the internet, and an administrator interface where blog owners log in to write new articles and manage their blogs. 
Figure 2.2 shows some of the key characteristics of these two sides.

Looking at the lists in figure 2.2, you can easily see a high level of conflict between the characteristics of the two sides. You’ve got content-rich, low interaction for the blog articles but a feature-rich, highly interactive environment for the admin interface.

The blog articles should be quick to load to reduce bounce rates, whereas the blog admin area should be quick to respond to user input and actions. Finally, users typically stay on a blog entry for a short time but may share it with others, whereas the admin interface is private, and an individual user could be logged in for a long time.

Taking what we’ve discussed about potential issues with SPAs and looking at the characteristics of blog entries, you’ll see quite a lot of overlap. Bearing this in mind, it’s likely that you wouldn’t choose to use an SPA to deliver your blog articles to readers. On the other hand, the admin interface is a perfect fit for an SPA. So what do you do? Arguably the most important thing is to keep the blog readers coming. If they get a bad experience, they won’t come back; neither will they share. If a blog doesn’t get readers, the writer will stop writing or move to another platform.

Then again, a slow and unresponsive admin interface will also see your blog owners jumping ship. So what do you do? How do you keep everybody happy and keep the blog engine in business?

### 2.3.2 A blog engine architecture

The answer lies in not looking for a one-size-fits-all solution. You effectively have two applications: public-facing content that should be delivered direct from the server and an interactive private admin interface that you want to build as an SPA. To start, look at the two applications separately, starting with the admin interface.

__ADMIN INTERFACE: AN ANGULAR SPA__

We’ve already stated that this interface would be an ideal fit for an SPA built in Angular.

The architecture for this part of the engine should look familiar: a REST API built with MongoDB, Express, and Node.js, with an Angular SPA up front. Figure 2.3 shows how this looks.

![](https://imgur.com/9l1R32T.png)


There’s nothing particularly new shown in figure 2.3. The entire application is built in Angular and runs in the browser, with JSON data being passed back and forth between the Angular application and the REST API.

__BLOG ENTRIES: WHAT TO DO?__

Looking at the blog entries, you can see that things get a little more difficult.
If you think of the MEAN stack only as an Angular SPA calling a REST API, you’re going to get a bit stuck. You could build the public-facing site as an SPA anyway, because you want to use JavaScript and the MEAN stack. But it’s not the best solution.
You could decide that the MEAN stack isn’t appropriate in this case and choose a different technology stack. But you don’t want to do that! You want end-to-end JavaScript.
Take another look at the MEAN stack, and think about all the components. You
know that Express is a web application framework. You know that Express can use template engines to build HTML on the server. You know that Express can use URL routing and MVC patterns. You should start to think that perhaps Express has the answer!

__BLOG ENTRIES: MAKING GOOD USE OF EXPRESS__

In this blog scenario, delivering the HTML and content directly from the server is exactly what you want to do. Express does this particularly well, even offering a choice of template engines right from the get-go. The HTML content will require data from the database, so you’ll use a REST API again. (For more on why it’s best to take this approach, see section 2.3.3.) 

Figure 2.4 lays out the basis for this architecture.

![](https://imgur.com/oIkA0dg.png)


This approach enables you to use the MEAN stack (or part of it, at least) to deliver database-driven content directly from the server to the browser. But it doesn’t have to stop there. The MEAN stack is even more flexible.

__BLOG ENTRIES: USING MORE OF THE STACK__

You’re looking at an Express application delivering blog content to visitors. If you want visitors to be able to log in, perhaps to add comments to articles, you need to track user sessions. You could use MongoDB with your Express application to do just this.
You might also have some dynamic data in the sidebar of your posts, such as related posts or a search box with type-ahead autocompletion. You could implement these in Angular. Remember, Angular isn’t only for SPAs; it can also be used to create individual components that add some rich data interactivity to an otherwise static page. 

Figure 2.5 shows these optional parts of MEAN added to the blog entry architecture.

![](https://imgur.com/Bwp7qEe.png)

Now you have the possibility of a full MEAN application delivering content to visitors who interact with your REST API.

__BLOG ENGINE: A HYBRID ARCHITECTURE__

At this point, you have two separate applications, each using a REST API. With a little bit of planning, you can have a common REST API used by both sides of the application.

Figure 2.6 shows what this looks like as a single architecture, with the single REST API interacting with the two front-end applications.

![](https://imgur.com/ooy3t9P.png)

This figure is a simple example to show how you can piece together the various parts of the MEAN stack into different architectures to answer the questions that your projects ask of you. Your options are limited only by your understanding of the components and your creativity in putting them together. There’s no one correct architecture for the MEAN stack.

### 2.3.3 Best practice: Building an internal API for a data layer

You’ve probably noticed that every version of the architecture includes an API to surface the data and allow interaction between the main application and the database.
There’s a good reason for this.

If you were to start by building your application in Node.js and Express, serving HTML directly from the server, it would be easy to talk to the database directly from the Node.js application code. With a short-term view, this way is the easy way. But with a long-term view, it becomes the difficult way, because it tightly couples your data to your application code in such a way that nothing else can use it.

The other option is to build your own API that can talk to the database directly and output the data you need. Then your Node.js application can talk with this API instead of directly with the database. 

Figure 2.7 shows a comparison of the two setups.

![](https://imgur.com/pvRX5DO.png)

Looking at figure 2.7, you could well be wondering why you’d want to go to the effort of creating an API just to sit between your application and your database. Isn’t it creating more work? At this stage, yes, it’s creating more work, but you want to look farther down the road. What if you want to use your data in a native mobile application or in an Angular front end later?

You certainly don’t want to find yourself having to write separate but similar interfaces for each. If you’ve built your own API up front that outputs the data you need, you can avoid this work. If you have an API in place, when you want to integrate the data layer into your application, you can simply make it reference your API. It doesn’t matter whether your application is Node.js, Angular, iOS, or Android. It doesn’t have to be a public API that anyone can use so long as you can access it. 

Figure 2.8 shows a comparison of the two approaches when you have Node.js, Angular, and iOS/Android applications all using the same data source.

![](https://imgur.com/RTcYhE1.png)

As figure 2.8 shows, the previously simple integrated approach is becoming fragmented and complex. You’ll have three data integrations to manage and maintain, so any changes will have to be made in multiple places to maintain consistency. If you have a single API, you don’t have any of these worries. With a little bit of extra work at the beginning, you can make life much easier for your future self. We’ll look at creating internal APIs in chapter 6.

## 2.4 Planning a real application

Working on a MEAN stack application, called __Loc8r__. Loc8r lists nearby places with Wi-Fi where people can go to get some work done. It also displays facilities, opening times, a rating, and a location map for each place. Visitors will be able to submit ratings and reviews.

For the sake of the demo application, you’ll create fake data so that you can test it quickly and easily. In the next section, we’ll walk you through the application planning. 


### 2.4.1 Planning the application at a high level

The first step is thinking about what screens you’ll need in your application. Focus on the separate page views and the user journeys. You can do this at a high level, not really concerning yourself with the details of what’s on each page. It’s a good idea to sketch out this stage on a piece of paper or a whiteboard, which helps you visualize the application as a whole. It also helps with organizing the screens into collections and flows while serving as a good reference point when you’re ready to build. As no data is attached to the pages or application logic behind them, it’s easy to add and remove parts, change what’s displayed where, and even change how many pages you want.

Chances are that you won’t get it right the first time; the key is to start, and then iterate and improve until you’re happy with the separate pages and overall user flow.

__PLANNING THE SCREENS__

Think about Loc8r. As stated earlier, your aim is as follows:

- Loc8r lists nearby places with Wi-Fi where people can go to get some work done. 
- It also displays facilities, opening times, a rating, and a location map for each place. 
- Visitors will be able to submit ratings and reviews.

From this description, you can get an idea about some of the screens you’re going to need:

- A screen that lists nearby places
- A screen that shows details about an individual place
- A screen for adding a review about a place
 
You’ll probably also want to tell visitors what Loc8r is for and why it exists, so you should add another screen to the list:
- A screen for “about us” information
  
__DIVIDING THE SCREENS INTO COLLECTIONS__

Next, take the list of screens and collate them where they logically belong together. 
- The first three screens in the list, for example, deal with locations. 
- The About page doesn’t belong anywhere, so it can go in a miscellaneous Others collection. 

A sketch of this arrangement looks something like figure 2.9.

![](https://imgur.com/L86H0c9.png)

Making a quick sketch like figure 2.9 is the first stage in planning, and you need to go through this stage before you can start thinking about architecture. This stage gives you a chance to look at the basic pages and think about the flow. 

Figure 2.9, for example, also shows a basic user journey in the Locations collection, going from the List page to a Details page and then to the form to add a review.

### 2.4.2 Architecting the application

On the face of it, Loc8r is a fairly simple application, with a few screens. But you still need to think about how to architect it, because you’re going to be transferring data from a database to a browser, letting users interact with the data, and allowing data to be sent back to the database.

__STARTING WITH THE API__

Because the application will use a database and pass data around, start building the architecture with the piece you’re definitely going to need. 

Figure 2.10 shows the starting point: a REST API built with Express and Node.js to enable interactions with the MongoDB database.

Building an API to interface with your data is a bit of a given and the base point of the architecture. The more interesting question is how you architect the application itself.

__APPLICATION ARCHITECTURE OPTIONS__

At this point, you need to take a look at the specific requirements of your application and how to put together the pieces of the MEAN stack to build the best solution. Do you need something special from MongoDB, Express, Angular, or Node.js that will swing the decision a certain way? Do you want HTML to be served directly from the server, or is an SPA a better option?

For Loc8r, you have no unusual or specific requirements, and whether it should be easily crawlable by search engines depends on the business growth plan. If the aim is to bring in organic traffic from search engines, yes, it needs to be crawlable. If the aim is to promote the application as an application and drive use that way, search engine visibility is a lesser concern.

Thinking back to the blog example, you can immediately envisage three possible
application architectures, as shown in figure 2.11:

![](https://imgur.com/ICmg6UP.png)

- A Node.js and Express application
- A Node.js and Express application with Angular additions for interactivity
- An Angular SPA

With these three options in mind, which is the best for Loc8r?


__CHOOSING AN APPLICATION ARCHITECTURE__

No specific business requirements are pushing you to favor one particular architecture over another. 
Building all three of the architectures allows you to explore how each approach works and enables you to take a look at each of the technologies in turn, building up the application layer by layer.

You’ll be building the architectures in the order in which they’re shown in figure 2.11, starting with a Node.js and Express application, and then adding some Angular before refactoring to an Angular SPA. Although this isn’t necessarily how you might build a site normally, it gives you a great opportunity to learn all aspects of the MEAN stack. In section 2.5, we’ll talk about this approach and walk through the plan in a bit more detail.

### 2.4.3 Wrapping everything in an Express project

The architecture diagrams that you’ve been looking at so far imply that you’ll have separate Express applications for the API and the application logic. This is perfectly possible and a good way to go for a large project. If you’re expecting large amounts of Database
JSON
API
Express
Node.js
MongoDB
JSON
Express application
Express
Node.js
Express and extras
Express
Node.js
Angular
Angular SPA
Angular
1. An Express and
Node.js application
2. An Express and
Node.js application
with additional
Angular components
3. An Angular SPA
Figure 2.11 Three options for building the Loc8r application, ranging from a server-side Express and Node.js application to a full client-side Angular SPA

traffic, you may even want your main application and your API on different servers.
An additional benefit of this approach is that you can have more specific settings for each of the servers and applications that are best suited to particular needs.
Another way is to keep things simple and contained by having everything inside a single Express project. With this approach, you have only one application to worry about hosting and deploying and one set of source code to manage. This is what do with Loc8r: creating one Express project that contains a few subapplications. Figure 2.12 illustrates this approach.

When you’re putting together an application in this way, it’s important to organize your code well so that the distinct parts of the application are kept separate. As well as making code easier to maintain, this makes it easier to split the code into separate projects if a future you decides that doing so is the right route. We’ll keep coming back to this key theme throughout the book.

### 2.4.4 The end product

As you can see, you use all layers of the MEAN stack to create Loc8r. You also include
Twitter Bootstrap to create a responsive layout. Figure 2.13 shows some screenshots of
what you’ll build throughout the book.
Database API
Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
Figure 2.12 The architecture of the application with the API and application logic wrapped inside
the same Express project
40 CHAPTER 2 Designing a MEAN stack architecture
2.5 Breaking the development into stages
In this book, you have two aims:
 Build an application on the MEAN stack.
 Learn about the different layers of the stack as you go.
You’ll approach the project in the way that you’d go about building a rapid prototype,
but with a few tweaks to give you the best coverage of the whole stack. Start by looking
Figure 2.13 Loc8r is the application you’ll build throughout this book. It displays differently on different
devices, showing a list of places and details about each place, and enables visitors to log in and leave
reviews.
Breaking the development into stages 41
at the five stages of rapid prototype development, and then see how to use this
approach to build up Loc8r layer by layer, focusing on the different technologies as
you go.
2.5.1 Rapid prototype development stages
The following sections break the process into stages, which lets you concentrate on
one thing at a time, increasing your chances of success. We find that this approach
works well for making an idea a reality.
STAGE 1: BUILD A STATIC SITE
The first stage is building a static version of the application, which is essentially several
HTML screens. The aims of this stage are
 To quickly figure out the layout
 To ensure that the user flow makes sense
At this point, you’re not concerned with a database or flashy effects on the user interface;
all you want to do is create a working mockup of the main screens and journeys
that a user will take through the application.
STAGE 2: DESIGN THE DATA MODEL AND CREATE THE DATABASE
When you have a working static prototype that you’re happy with, the next thing to do
is look at any hardcoded data in the static application, and put it in a database. The
aims of this stage are
 To define a data model that reflects the requirements of the application
 To create a database to work with the model
The first part is defining the data model. Stepping back to a bird’s-eye view, what are
the objects you need data about, how are the objects connected, and what data is held
in them?
When you try to do this stage before building the static prototype, you’re dealing
with abstract concepts and ideas. When you have a prototype, you can see what’s happening
on different pages and what data is needed where. Suddenly, this stage
becomes much easier. Almost unknown to you, you’ve done the hard thinking while
building the static prototype.
STAGE 3: BUILD YOUR DATA API
After stages 1 and 2, you have a static site on one hand and a database on the other.
This stage and the next take the natural steps of linking them. The aim of stage 3 is
 To create a RESTful API that allows your application to interact with the database
STAGE 4: HOOK THE DATABASE INTO THE APPLICATION
When you get to this stage, you have a static application and an API exposing an interface
to your database. The aim of this stage is
 To get your application to talk to your API
42 CHAPTER 2 Designing a MEAN stack architecture
When this stage is complete, the application will look pretty much the same as it did
before, but the data will be coming from the database. When it’s done, you’ll have a
data-driven application!
STAGE 5: AUGMENT THE APPLICATION
This stage is all about embellishing the application with additional functionality. You
might add authentication systems, data validation, or methods for displaying error
messages to users. This stage could include adding more interactivity to the front end
or tightening the business logic in the application.
The aims of this stage are
 To add finishing touches to your application
 To get the application ready for people to use
These five stages of development provide a great methodology for approaching a new
build project. In the next section, you’ll take a look at how you’ll follow these steps to
build Loc8r.
2.5.2 The steps to build Loc8r
In building Loc8r throughout this book, you have two aims. First, of course, you want
to build a working application on the MEAN stack. Second, you want to learn about
the different technologies, how to use them, and how to put them together in different
ways.
Throughout the book, you’ll follow the five stages of development, but with a couple
of twists so that you get to see the whole stack in action. Before looking at the steps
in detail, quickly remind yourself of the proposed architecture shown in figure 2.14.
Database API
Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
Figure 2.14 Proposed architecture for Loc8r
as you’ll build it throughout this book
Breaking the development into stages 43
STEP 1: BUILD A STATIC SITE
You’ll start by following stage 1 and building a static site. We recommend doing this
for any application or site, because you can learn a lot with relatively little effort.
When building the static site, it’s good to keep one eye on the future, keeping in mind
what the final architecture will be. The architecture for Loc8r is already defined, as
shown in figure 2.14.
Based on this architecture, you’ll build the static application in Node and Express,
using that as your starting point into the MEAN stack. Figure 2.15 highlights this step
in the process as the first part of developing the proposed architecture. This step is
covered in chapters 3 and 4.
STEP 2: DESIGN THE DATA MODEL AND CREATE THE DATABASE
Still following the stages of development, you’ll continue to stage 2 by creating the
database and designing the data model. Again, any application is likely to need this
step, and you’ll get much more out of it if you’ve been through step 1 first.
Figure 2.16 illustrates how this step adds to the overall picture of building up the
application architecture.
In the MEAN stack, you’ll use MongoDB for this step, relying heavily on Mongoose
for the data modeling. The data models are actually defined inside the Express application.
This step is covered in chapter 5.
Database API
Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
1. Build a static
app with
Express and
Node.js.
Figure 2.15 The starting point for your
application is building the user interface in
Express and Node.js.
44 CHAPTER 2 Designing a MEAN stack architecture
STEP 3: BUILD YOUR REST API
When you’ve built the database and defined the data models, you’ll want to create a
REST API so that you can interact with the data through making web calls. Pretty
much any data-driven application will benefit from having an API interface, so this
step is another one you’ll want to have in most build projects.
You can see where this step fits into building the overall project in figure 2.17.
Database Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
API
2. Create a database and
design a data model.
Figure 2.16 After the static site is built, you’ll use
the information gleaned to design the data model and
create the MongoDB database.
Database API
Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
to expose the
database.
3. Build an API
Figure 2.17 Use Express and Node.js to build
an API, exposing methods of interacting with
the database.
Breaking the development into stages 45
In the MEAN stack, this step is done mainly in Node.js and Express, with quite a bit of
help from Mongoose. You’ll use Mongoose to interface with MongoDB rather than
deal with MongoDB directly. This step is covered in chapter 6.
STEP 4: USE THE API FROM YOUR APPLICATION
This step matches stage 4 of the development process and is where Loc8r starts to
come to life. The static application from step 1 will be updated to use the REST API
from step 3 to interact with the database created in step 2.
To learn about all parts of the stack and the different ways in which you can use
them, you’ll use Express and Node.js to make calls to the API. If, in a real-world scenario,
you planned to build the bulk of an application in Angular, you’d hook your
API into Angular instead. That approach is covered in chapters 8, 9, and 10.
At the end of this step, you’ll have an application running on the first of the three
architectures: an Express and Node.js application. Figure 2.18 shows how this step
glues together the two sides of the architecture.
In this build, you’ll do the majority of this step in Node.js and Express. This step is covered
in chapter 7.
STEP 5: EMBELLISH THE APPLICATION
Step 5 relates to stage 5 in the development process, where you get to add extra
touches to the application. You’ll use this step to take a look at Angular and see how
you can integrate Angular components into an Express application. This addition to
the project architecture is highlighted in figure 2.19.
Database API
Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
4. Hook the Express
application into
the data API.
Figure 2.18 Update the static Express
application by hooking it into the data API,
allowing the application to be database-driven.
46 CHAPTER 2 Designing a MEAN stack architecture
This step is all about introducing and using Angular. To support this step, you’ll most
likely also change some of your Node.js and Express setup. This step is covered in
chapter 8.
STEP 6: REFACTOR THE CODE INTO AN ANGULAR SPA
In step 6, you’ll radically change the architecture by replacing the Express application
and moving all the logic into an SPA, using Angular. Unlike the previous steps, this
step replaces some of what came before it rather than building on it.
This step would be an unusual one in a normal build process—to develop an application
in Express and redo it in Angular—but it suits the learning approach in this
book particularly well. You’ll be able to focus on Angular, as you already know what
the application should do, and a data API is ready for you to use.
Figure 2.20 shows how this change affects the overall architecture. This step once
again focuses on Angular and is covered in chapters 9 and 10.
STEP 7: ADD AUTHENTICATION
In step 7, you’ll add functionality to the application by enabling users to register and
log in. You’ll also see how to make use of users’ data while they’re using the application.
You’ll build on everything you’ve done so far and add authentication to the
Angular SPA. As part of this step, you’ll save user information in the database and
secure certain API endpoints so that they can be used only by authenticated users.
Figure 2.21 shows what you’ll be working with in the architecture. In this step, you’ll
work with all the MEAN technologies. This step is covered in chapters 11 and 12.
That’s the planned software architecture. In the next section, we’ll have a quick
chat about hardware.
Database API
Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
5. Add the Angular
components to
the front end.
Figure 2.19 One way to use Angular in a MEAN
application is to add components to the front end
in an Express application.
Breaking the development into stages 47
Database API
Express application
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
6. Refactor the code
into an Angular SPA.
Figure 2.20 Effectively rewriting the application as an Angular SPA
Database API
Express
Node.js
Angular
Angular SPA
Angular
Express
Node.js
MongoDB
Express application
7. Use the whole MEAN
stack to add authentication
to the Angular SPA.
Figure 2.21 Using all the MEAN stack to add authentication to the Angular SPA
48 CHAPTER 2 Designing a MEAN stack architecture
2.6 Hardware architecture
No discussion of architecture would be complete without a section on hardware.
You’ve seen how the software and code components can be put together, but what
type of hardware do you need to run it all?
2.6.1 Development hardware
The good news is that you don’t need anything particularly special to run a development
stack. A single laptop or even a virtual machine (VM) is enough to develop a
MEAN application. All components of the stack can be installed on Windows, macOS,
and most Linux distributions.
We’ve successfully developed applications on Windows and macOS laptops, as well
as on Ubuntu VMs. Our preference is native development on macOS, but we know
others who swear by Linux VMs.
If you have a local network and several servers, you can run different parts of your
application across them. It’s possible to have one machine as a database server,
another for the REST API, and a third for the main application code itself, for example.
So long as the servers can talk to one another, this setup isn’t a problem.
2.6.2 Production hardware
The approach to production hardware architecture isn’t all that different from development
hardware. The main difference is that production hardware is normally
higher-spec and open to the internet to receive public requests.
STARTER SIZE
It’s possible to have all parts of your application hosted and running on the same
server. You can see a basic diagram in figure 2.22.
This architecture is okay for applications with low traffic but isn’t generally advised as
your application grows, because you don’t want your application and database fighting
over the same resources.
GROWING UP: A SEPARATE DATABASE SERVER
One of the first things moved to a separate server is often the database. Now you have
two servers: one for the application code and one for the database. Figure 2.23 illustrates
this approach.
Database REST API Application
Figure 2.22 The simplest of
hardware architectures, with
everything on a single server
Hardware architecture 49
This model is common, particularly if you choose to use a Platform as a Service (PaaS)
provider for your hosting. You’ll use that approach in this book.
GOING FOR SCALE
Much as we talked about in the section on development hardware, you can have a different
server for the different parts of your application: a database server, an API
server, and an application server. This setup allows you to deal with more traffic as the
load is spread across three servers, as illustrated in figure 2.24.
But it doesn’t stop there. If your traffic starts to overload your three servers, you can
have multiple instances (or clusters) of these servers, as shown in figure 2.25.
Database REST API Application
Figure 2.23 A common hardware
architecture approach: one server to
run the application code and API and a
second, separate database server
Database REST API Application
Figure 2.24 A decoupled architecture using three servers: one for the
database, one for the API, and one for the application code
Database REST API Application
Figure 2.25 You can scale
MEAN applications by having
clusters of servers for each
part of your entire application.
50 CHAPTER