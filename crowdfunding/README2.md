<h1><img src=../../global_images/logo.png width="100" />Intro To Django and DRF<img src=../../global_images/logo.png width="100" /></h1>

Welcome to the Django and Django Rest Framework Unit! This unit and the next unit (JavaScript and React) work together. Your project for this unit will be to create *half* of a website (the back half). In the JavaScript and React unit, your project will be to create the front half! 

That might sound a little confusing, but don't worry - this block of content is here to give you some framing around it.

> [!IMPORTANT]  
> There's a lot of theory and jargon packed into this lesson. We recommend absorbing as much as you can in class, and then returning to these notes frequently to refresh yourself as you progress through the unit.

<h2>Table of Contents</h2>

- [1 - 🧑‍🏫 What We Are Learning 🧑‍🏫](#1----what-we-are-learning-)
- [2 - 💬 HTTP: How Websites Communicate 💬](#2----http-how-websites-communicate-)
- [3 - ✨ Dynamic Web Content ✨](#3----dynamic-web-content-)
- [4 - 🥞 The Full Stack Development Paradigm 🥞](#4----the-full-stack-development-paradigm-)
  - [4.1 - 🖥️ Client-Side Computing (Front-End) 🖥️](#41---️-client-side-computing-front-end-️)
  - [4.2 - ☁️ Server-Side Computing (Back-End) ☁️](#42---️-server-side-computing-back-end-️)
- [5 - 🤔 Where Do Django and DRF Come In? 🤔](#5----where-do-django-and-drf-come-in-)
  - [5.1 - 🕺 Django 💃](#51----django-)
  - [5.2 - 🛏️ Django Rest Framework 🛏️](#52---️-django-rest-framework-️)
- [6 - 🕵️ How Django and DRF Do It 🕵️](#6---️-how-django-and-drf-do-it-️)
  - [6.1 - 💾 Database 💾](#61----database-)
  - [6.2 - 🛠️ Models 🛠️](#62---️-models-️)
  - [6.3 - 🥣 Serializers 🥣](#63----serializers-)
  - [6.4 - 🧑‍🍳 Views 🧑‍🍳](#64----views-)
- [7 - 🧩 Putting It All Together 🧩](#7----putting-it-all-together-)
  - [An Example](#an-example)

## 1 - 🧑‍🏫 What We Are Learning 🧑‍🏫
So far while we've been learning Python, we've been using what you might call "Vanilla Python". That is, we've been sticking to the tools and features that ship in Python's *Standard Library*. These are the heart of Python, and once you begin to understand even a few of them you are a programmer, no take-backsies.

But one of the best things about Python is the enormous community of people from all over the world who use Python to create powerful *new* tools for niche applications!

Think about this - for your project last unit you wrote a set of functions that converted CSV files into text outputs. Those functions could be really useful in a number of different applications! If you wanted to, you could package them up and share them with the world, so that other people who wanted to work with weather data could decide to use them in their programs.

That's what Django and Django Rest Framework are. They're two sets of tools, written in Python, that are designed to help people create websites. 

Django sets itself apart with its "batteries included" approach, where it aims to provide tools to do every single part of the work of website creation. Ideally this means that once you learn the ropes, all of the questions you need to answer when you're making your websites will be of the form "*what sort of website do I want to make?*". You should rarely have to ask yourself a question like "*how can I write Python code that performs this common website task?*".

Of course, we still need to learn how to use the tools that Django/DRF give us. And that's what this unit is about, so let's get to it!

---
---

## 2 - 💬 HTTP: How Websites Communicate 💬
HTTP stands for "*HyperText Transfer Protocol*".  

A "protocol" is a defined way for computers to communicate with each other. HTTP is the main protocol that we use for website data transfer.

When you access a website through a browser, your computer (called the "**client**") sends a message called an **HTTP GET Request** out over the internet, asking for the file/s that represent the site.

![](./img/http_request.drawio.png)
> This type of HTTP request is called a "GET" request.

Your request is bounced to another computer somewhere called a "**server**", which has been given the job of distributing the website HTML files. It sends back a **response** containing the website page you requested.

![](./img/http_response.drawio.png)
> The HTTP response contains the HTML code for the site.

For the websites you have been making so far, that has been enough. This unit is our first look at some more powerful website creation, which means we need a more complex way of communicating between the client and the server.

Luckily, GET requests aren't the only type of request we have available. HTTP provides various types of requests, each of which fulfils a different purpose:

| Request Type | Purpose                                    |
| ------------ | ------------------------------------------ |
| **GET**      | Retrieves website data from the server.    |
| **POST**     | Sends data *to* the server to be recorded. |
| **PUT**      | Updates a stored record.                   |
| **PATCH**    | *Partially* updates a stored record.       |
| **DELETE**   | Deletes a stored record.                   |

> There are even more request types than these, but we won't use them in this course.

So why do we need this more complex set of request types?

---
---

## 3 - ✨ Dynamic Web Content ✨
Dynamic websites are why we need all of these HTTP request types!

The portfolio sites that you made in your first project were what we call "*static websites*". That means that once you finish writing them and deploy, they're always the same for every user who visits them, unless you go back and make a change to the code. 

Static websites are really useful! But most of the websites you visit on the internet are not static. Instead they are ✨*dynamic*✨.

Think about Instagram. Your Instagram feed is different every time you visit it. There are new posts to see and new friends to add, and you can interact with the website to change what you and your followers see! You yourself can change the contents of Instagram dot com, by uploading a new photo, editing an old post, or deleting one of your contacts.

When you upload a photograph to Instagram, your browser is making a POST request - sending the photo to the server to be stored. When you edit a comment on Instagram, you are making a PUT request - replacing your old comment text with something new. 

My friends, Instagram is written with Django.

Clearly there's a lot of complex logic built into dynamic web content. So how do we manage that complexity?

---
---

## 4 - 🥞 The Full Stack Development Paradigm 🥞
The "full stack" paradigm is one of the coding paradigms that allows us to manage the complexity of dynamic websites!

This involves "splitting up the work" of generating our website between the server computer and the client computer. These two halves communicate with each other through an ***"API"***. 

API stands for ***"Application Programming Interface"***. That's computer science jargon for "a way for two programs to talk to one another".

> [!NOTE]  
> The full stack method isn't the only way to create a dynamic website! It's not even the only way to create a dynamic website using Django. 😎 

---

### 4.1 - 🖥️ Client-Side Computing (Front-End) 🖥️
Code always has to run on a computer. The big question is - whose? 

Code like Javascript can be run by a web-browser, which means it can be sent to a user as part of a website, and run on **their** computer. This is called "*client-side*" computing. When we get to the React lessons later in this course, we'll be writing code for the client-side.

Most client-side code revolves around managing ***how content is displayed to the user***. For this reason, it gets called "**front-end**" code, because it goes up front where the user can see it.

---

### 4.2 - ☁️ Server-Side Computing (Back-End) ☁️
Python, on the other hand, can't run in the browser. This means that we can't send it to the user as part of a website. Instead, when we want to use Python code in a website, we use another computer on the internet to run it. This computer is called a "server", and the code that runs on it is "*server-side*" code. 

Since Django is a Python tool, all the code we write with it will be server-side code! We call this code "**back-end**" code, because it runs behind the scenes on the server.

Most back-end code revolves around ***storing and retrieving information***. When the front-end sends user-supplied data through, the back-end API recieves it and stores it. When the front-end wants to display some stored information, it sends a request to the back-end, and the back-end supplies the info! 

---
---

## 5 - 🤔 Where Do Django and DRF Come In? 🤔
Let's look at how we'll actually deliver that full-stack website.

---

### 5.1 - 🕺 Django 💃
Django lets us build **server-side** code for **dynamic** websites. 

If you want to, you can make a website with *just* Django. To do this you write code that auto-generates HTML pages, using a technique called "*templating*". Every time the user clicks a button on the front-end, a request is sent to your server, and the Django code you wrote sends through a freshly-generated HTML page to display to the user. 

Using Django on its own works fine, but it is a little clunky. Even a small change to the website requires the user to wait for the server to respond with a whole new page.

Luckily, in the next unit we are planning to create some React code on the front end of our websites. That code will handle the task of generating HTML to display to the user. That means that we won't be doing any templating in this course. Instead, we just need our back-end to handle the record storage, and respond to front-end requests for data.

---

### 5.2 - 🛏️ Django Rest Framework 🛏️
Django handles the data storage just fine, but on its own it isn't designed to communicate with a React front-end. Enter Django Rest Framework! 

DRF is designed to extend the functionality of Django by adding in the tools to create **REST API Endpoints**. A REST API is an interface that lets the front-end talk to the back-end!

We'll discuss APIs in some more depth in this week's masterclass. For now, it's enough to know that DRF is the extra spice that allows us to hook our Django code up to the React front-end that we will build in the next unit.

---
---

## 6 - 🕵️ How Django and DRF Do It 🕵️
We could probably write all of the code for our back-end in one giant file, but it would be messy and very hard to troubleshoot. Instead, programmers like to break the work up into sensible chunks, and assign each "job" to a different part of the program. 

We will be creating three major "chunks": **Models**, **Views**, and **Serializers**. 

Below is a diagram of how these components fit together. It won't make much sense yet, but we are going to work through each component right now and quickly explain what they all mean. Then as we build out our project during class time, we'll create each component and learn how their code fits together!

![](./img/fullstack_flow.drawio.png)
> This diagram is called a "Data Flow Diagram" because it describes how the program moves information around to produce its output.

---

### 6.1 - 💾 Database 💾
We've mentioned storing information a few times in this document so far. Right now you might be thinking, "Storing information? That's what variables are for!"

Variables are great, but in some situations they don't quite cut it.

- When a program stops running (or crashes), any data that was stored in a variable gets lost forever. 
- There's a limit to how much data we can store in variables. Instagram has well over 2 billion users - there's no computer in the world big enough to handle all that data in variables. 

This means that we need something more powerful Instead of variables, we need to use *databases*.

A database is basically a giant hard drive that stores data and makes them available to programs. There are a few different ways that databases organise their data, but the most common type is a *relational database*, and that's what we will be using in this course.

---

### 6.2 - 🛠️ Models 🛠️
When we use Django, we almost never have to interact with the database directly. Instead, we write Python classes called "**models**", and Django creates a database table for us based on them. 

Each model class corresponds to one type of fact that gets recorded in the database. Instagram would have a model for users, a model for images, a model for comments, etc... 

When we want to retrieve data about users from the database, we grab our `User` model, and tell it to give us the data. It talks to the database for us and spits out a bunch of `User` instances based on the information stored there. Then we can use those instances in our program!

---

### 6.3 - 🥣 Serializers 🥣
When our models retrieve data for us, they come as Python class instances. That's great for us, but our React front-end doesn't understand Python. We need to translate those class instances into something that the front-end will understand. 

Serializers do this work of translation. They use a notation called ***JSON*** to represent data so that it can be sent between our Python/Django back-end and the React front-end.

We'll learn more about JSON in an upcoming masterclass!

---

### 6.4 - 🧑‍🍳 Views 🧑‍🍳
So far we have a collection of data stored in our database, accessed by models, and converted to transmissible objects by serializers. That doesn't accomplish much without some logic to decide which models and serializers get used, and how.  

The chunks of code we use for this key task are the "**views**". 

Views are our decision-makers. Like the head chef in a restaurant, they recieve requests, and then order the models and serializers (the sous chefs) to prepare ingredients for them. Finally they perform the magic of combining it all, and serve it back to the user.

---
---

## 7 - 🧩 Putting It All Together 🧩
Let's see that data flow diagram again. Have a go at tracing the path of the data through the program, and pondering what is happening at each step. Feel free to grab a mentor and quiz them if anything is unclear!

![](./img/fullstack_flow.drawio.png)

> [!IMPORTANT]  
> We know this is all very abstract right now!
>
> Don't worry, you don't need to leave this lesson understanding everything that we talked about here. We will build an example back-end over the next few lessons that will give you a practical demonstration of these ideas. Then you'll be ready to apply the theory by customising this example back-end to suit your own plans. We expect you to continue building your knowledge of how back-ends work throughout this unit, and into the next one!

### An Example 
The following links show off the completed example back-end that we'll build over the next few lessons. The data you see displayed here are exactly what a React front-end might request:

- [An API endpoint that lists all users](https://solitary-glitter-2281.fly.dev/users/)
- [An API endpoint that lists all projects](https://solitary-glitter-2281.fly.dev/projects/)

![The She Codes Logo](../../global_images/logo.png)

# Django Rest Framework Project: Crowdfunding App (Part 1)<br><sub><sup><sub>Due: Last Sunday of the module at 11:59pm.</sub></sup></sub>

## Project Description
Kickstarter, Go Fund Me, Kiva, Change.org, Patreon… All of these different websites have something in common: they provide a platform for people to fund projects that they believe in, but they all have a slightly different approach. You are going to create your own crowdfunding website, and put your own spin on it!

## Project Requirements
Your crowdfunding project must:

- [ ] Be separated into two distinct projects: an API built using the Django Rest Framework and a website built using React. 
- [ ] Have a cool name, bonus points if it includes a pun and/or missing vowels. See https://namelix.com/ for inspiration. <sup><sup>(Bonus Points are meaningless)</sup></sup>
- [ ] Have a clear target audience.
- [ ] Have user accounts. A user should have at least the following attributes:
  - [ ] Username
  - [ ] Email address
  - [ ] Password
- [ ] Ability to create a “project” to be crowdfunded which will include at least the following attributes:
  - [ ] Title
  - [ ] Owner (a user)
  - [ ] Description
  - [ ] Image
  - [ ] Target amount to fundraise
  - [ ] Whether it is currently open to accepting new supporters or not
  - [ ] When the project was created
- [ ] Ability to “pledge” to a project. A pledge should include at least the following attributes:
  - [ ] An amount
  - [ ] The project the pledge is for
  - [ ] The supporter/user (i.e. who created the pledge)
  - [ ] Whether the pledge is anonymous or not
  - [ ] A comment to go along with the pledge
- [ ] Implement suitable update/delete functionality, e.g. should a project owner be allowed to update a project description?
- [ ] Implement suitable permissions, e.g. who is allowed to delete a pledge?
- [ ] Return the relevant status codes for both successful and unsuccessful requests to the API.
- [ ] Handle failed requests gracefully (e.g. you should have a custom 404 page rather than the default error page).
- [ ] Use Token Authentication, including an endpoint to obtain a token along with the current user's details.
- [ ] Implement responsive design.

## Additional Notes
No additional libraries or frameworks, other than what we use in class, are allowed unless approved by the Lead Mentor.

Note that while this is a crowdfunding website, actual money transactions are out of scope for this project.

## Submission
To submit, fill out [this Google form](https://forms.gle/34ymxgPhdT8YXDgF6), including a link to your Github repo. Your lead mentor will respond with any feedback they can offer, and you can approach the mentoring team if you would like help to make improvements based on this feedback!

Please include the following in your readme doc:
- [ ] A link to the deployed project.
- [ ] A screenshot of Insomnia, demonstrating a successful GET method for any endpoint.
- [ ] A screenshot of Insomnia, demonstrating a successful POST method for any endpoint.
- [ ] A screenshot of Insomnia, demonstrating a token being returned.
- [ ] Step by step instructions for how to register a new user and create a new project (i.e. endpoints and body data).
- [ ] Your refined API specification and Database Schema.

<h1><img src=../../global_images/logo.png width="100" />Intro To Databases<img src=../../global_images/logo.png width="100" /></h1>
Databases could have a whole course of their own.

We don't need to do a proper deep dive, but it's important to know what's going on in them. We'll be using *relational* databases in this course, so that's what we'll focus on here.

<h2>Table Of Contents</h2>

- [Tables](#tables)
  - [Example User Table](#example-user-table)
- [SQL](#sql)
- [Database Schemas](#database-schemas)
  - [First Normal Form](#first-normal-form)
  - [ERD](#erd)


![](./img/database.drawio.png)
> For some reason, a segmented cylinder like these is the symbol that the world has settled on to represent a database. It's fine, I guess.

## Tables
A relational database organises its data into a series of **tables**. These are kind of like Excel spreadsheets. 

Each table contains one type of data. So for a website like Instagram, we would have a table for users, a table for comments, a table for likes, etc...

Here's what a table for users might look like on some website, somewhere:

### Example User Table
| UserID | Name    | Occupation  | Username                     | Birthdate  |
| ------ | ------- | ----------- | ---------------------------- | ---------- |
| 1      | Bilbo   | Burglar     | barrel_rider                 | 20/07/1948 |
| 2      | Thorin  | King        | oakenshield                  | 30/05/1916 |
| 3      | Balin   | Miner       | platesmash                   | 29/09/1934 |
| 4      | Dwalin  | Musician    | violaihardlyknowher          | 02/03/1917 |
| 5      | Oin     | Outdoorsman | n_not_k                      | 21/05/1904 |
| 6      | Gloin   | Outdoorsman | l_not_r                      | 23/10/1974 |
| 7      | Dori    | Musician    | blowhard                     | 26/01/1933 |
| 8      | Nori    | Musician    | like_the_seaweed             | 28/03/1964 |
| 9      | Ori     | Musician    | could_probably_use_a_warrior | 04/01/1935 |
| 10     | Bifur   | Musician    | seriously_just_one_fighter   | 22/09/1950 |
| 11     | Bofur   | Musician    | bofur_deez                   | 22/07/1942 |
| 12     | Bombur  | Miner       | dont_drink_the_water         | 27/02/1904 |
| 13     | Fili    | Musician    | thefiddlerunderthemountain   | 03/12/1916 |
| 14     | Kili    | Musician    | dis_graceful_son             | 16/01/1972 |
| 15     | Gandalf | Wizard      | olorin                       | 12/04/1990 |

> Once again, the characters from the Hobbit come in clutch in our example. Unfortunately we have to use randomly generated birthdays, since the calendar system in Middle Earth doesn't align with our own.

Tables table are made up of **columns** and **rows**. 
- Each column holds a type of fact: `Name`, `Occupation`, etc.
- Each row holds a record: a person, a product for sale, etc. 

A cell at the intersection of a row and a column is called a "**field**". So here we would say that record #1 has the value `"Bilbo"` in its `Name` field. 

The first column in this table contains a unique ID that can be used to identify the user in that row. This is called a "**Primary Key**".

## SQL
When we want to get information from the database, we construct a "*query*" in a language called **SQL** (**S**tructured **Q**uery **L**anguage). We send this query to the database, and it responds with the data we requested. 

SQL isn't a programming language like Python, but it is still very powerful and useful. We won't deep dive on it in this course, but just in case you're curious, here's an example of what an SQL query might look like:

```SQL
SELECT * FROM Users WHERE Occupation = 'Musician';
```
> This says something like "Get me every column from the rows that have a value of `'Musician'` in the `Occupation` field."

And the result, depicted here in CSV format:
```CSV                           
4,Dwalin,Musician,violaihardlyknowher,02/03/1917
7,Dori,Musician,blowhard,26/01/1933
8,Nori,Musician,like_the_seaweed,28/03/1964
9,Ori,Musician,could_probably_use_a_warrior_in_here,04/01/1935
10,Bifur,Musician,seriously_just_one_fighter,22/09/1950
11,Bofur,Musician,bofur_deez,22/07/1942
13,Fili,Musician,thefiddlerunderthemountain,03/12/1916
14,Kili,Musician,dis_graceful_son,16/01/1972
```

## Database Schemas
When we store information in a database, we are generally not storing random, unrelated facts. Most of the time, the data in one table relate to data in another table. This is why it's called a *relational* database!

The **schema** of a database describes the structure of the data that are stored in it, and the relationships between them. 

For instance, in J.R.R Tolkien's *The Hobbit*, a lot of time is dedicated to describing all the delicious things that the characters eat and drink. If I wanted to, I could go through the book and collect data on all the food that the characters ate. Then I could add this *related* information to the database that contains the user data we described above.

### First Normal Form
Relational databases have a crucial constraint: *field values must be "atomic"*!

"Atomic" in this context means "indivisible or singular". As in, you can only put **one** value in a field in a database table. 
 
A number? Fine. A string? Great. A date? Perfect! 

A list, or a dictionary, or some other iterable data type? **NOPE**. These are not allowed. 

This rule is called the "**First Normal Form**" of relational databases, or "**1NF**" for short.

According to 1NF, if we want to add the meal data to our database then we **can't** just add an extra column to the existing `Users` table, and fill it with lists of all the food each person eats. That's not allowed, because lists contain multiple values, so they aren't "atomic" data.

Instead, we create a new table, with each row containing a description of a food item. In this table, we add an extra column to contain the primary key of the user who ate the food. Like this:

![](./img/schema.drawio.png)

The data here are *related*. The IDs in the `DinerID` column of my `Meals` table correspond to individual people. And those people are represented by *rows* in my `Users` table! 

- When you want to know who ate a meal, you check the `DinerID` field of its row, and then look up that primary key in the `Users` table.
- When you want to know what a given user ate, you check their `UserID`, and then grab all the `Meals` records that have that value for their `DinerID`.

> [!NOTE]  
> There are actually five normal forms. Together they provide advice for creating well-structured databases. If you're looking to learn a little more about them, [this video provides a great explanation.](https://www.youtube.com/watch?v=GFQaEYEc8_8)

### ERD
When we want to depict a schema like the one we just described, we use an **E**ntity **R**elationship **D**iagram. ("ERD" for short.)

The "**entities**" here are "the categories of things that we are recording data about". People, meals, etc.  An ERD for the tables we just described might look like this:

![](./img/erd.drawio.png)

Here's a version with some annotations to explain what's going on in the diagram:

![](./img/annotated_erd.drawio.png)


<h1><img src=../../global_images/logo.png width="100" />😴 Insomnia 😴<img src=../../global_images/logo.png width="100" /></h1>
Although it might sound like a problem to talk to your doctor about, Insomnia is also the name of a very useful app for web developers! 

It is an API testing tool, that lets you send requests to your back end and see its responses, without having a front end website first.

This is great, because it means we can work on the back end now, and then create the front end once we are ready.

We need a tool like this because our back end won't be designed for human beings to access it. It will be designed for other computers to access! Normally the front end code we write would do this work, but before it is written, we can use Insomnia.

> [!NOTE]  
> Another tool for this work is called Postman - they both do roughly the same thing!

---
---
---

<h2>Table Of Contents</h2>

- [1 -📥 Installing 📥](#1---installing-)
- [2 - 🗺️ Insomnia's Layout 🗺️](#2---️-insomnias-layout-️)
	- [2.1 - 🏢 Organisations 🏢](#21----organisations-)
	- [2.2 - 🏗️ Projects 🏗️](#22---️-projects-️)
	- [2.3 - 🗂️ Collections 🗂️](#23---️-collections-️)
- [3 - 🛏️ Using Insomnia 🛏️](#3---️-using-insomnia-️)
	- [3.1 - 🏢 Your Organisation 🏢](#31----your-organisation-)
	- [3.2 - 🏗️ Creating A Project 🏗️](#32---️-creating-a-project-️)
	- [3.3 - 🗂️ Creating A Collection 🗂️](#33---️-creating-a-collection-️)
	- [3.4 - 🫴 Creating A GET Request 🫴](#34----creating-a-get-request-)
		- [3.4.1 - Specifying The Request URL](#341---specifying-the-request-url)
		- [3.4.2 - Receiving The Response](#342---receiving-the-response)
	- [3.5 - 📨 Creating A POST Request 📨](#35----creating-a-post-request-)
		- [3.5.1 - A Different Request URL](#351---a-different-request-url)
		- [3.5.2 - A Different REST Verb](#352---a-different-rest-verb)
		- [3.5.3 - Adding JSON Data To The Request Body](#353---adding-json-data-to-the-request-body)
		- [3.5.4 - Receiving The Response](#354---receiving-the-response)

---
---
---

## 1 -📥 Installing 📥
If you haven't got it already, you can download and install Insomnia here: https://insomnia.rest/download

---
---
---

## 2 - 🗺️ Insomnia's Layout 🗺️
Insomnia operates on a system of "Organisations", "Projects", and "Collections"

---
---

### 2.1 - 🏢 Organisations 🏢
Organisations are at the top level of the Insomnia's structure. You can select them in the leftmost vertical ribbon in the Insomnia interface:

![](./img/insomnia_layout1.png)

---
---

### 2.2 - 🏗️ Projects 🏗️
Projects are the next level down in Insomnia's structure. Each project corresponds to a single app or website you are creating. 

This means you should create a new Insomnia project for your Crowdfunding project, and for each new app you work on after that.

You can create and select projects in the left-hand pane of the Insomnia interface:

![](./img/insomnia_layout2.png)

---
---

### 2.3 - 🗂️ Collections 🗂️
A collection is a set of HTTP requests that you are working on to test some aspect of your project. You can define multiple requests in a collection, and issue them repeatedly to test your back end.

---
---
---

## 3 - 🛏️ Using Insomnia 🛏️
Let's work through an example of how to use Insomnia!

---
---

### 3.1 - 🏢 Your Organisation 🏢
It's possible that if this is your first time installing insomnia, you will need to create an organisation to work in. (This depends on your installation.)

Calling your org "personal projects" or something similar is fine. 

You shouldn't have to do this again on this computer - one organisation will be enough for you, until you get a job as a developer!

---
---

### 3.2 - 🏗️ Creating A Project 🏗️
Let's create a project now. You can call it "Demo". 

You should have one project for each website you are working on.

---
---

### 3.3 - 🗂️ Creating A Collection 🗂️
Since this is a new project, you can create a new collection by clicking the button in the center of the main pane in the Insomnia interface:

![](./img/insomnia_layout3.png)

Create a collection now. You can call it "Demo" as well.

This will transport you to the collection view:

![](./img/insomnia_layout4.png)

You can have multiple collections for each project. This is useful for keeping requests organised when you are testing multiple different features.

> If you need to, you can always return to your Org view to create new projects and collections by clicking on the Organisation in the leftmost ribbon.

---
---

### 3.4 - 🫴 Creating A GET Request 🫴
Click the small `(+)` button at the top of the leftmost pane to create a new request:

![](./img/insomnia_layout6.png)

We want to create an HTTP Request! If you want to, you can give yours a name, but since this is just a demo, I will leave mine with the default.

---

#### 3.4.1 - Specifying The Request URL
Every request needs to be sent to a specific "API endpoint". This is a URL where a back-end program is listening for requests, ready to respond to them. Since you haven't built API of your own yet, you can use this demo:

```
https://solitary-glitter-2281.fly.dev/
```

Paste the above link into the URL bar of your new request, and hit the `Send` button!

![](./img/insomnia_layout7.png)

---

#### 3.4.2 - Receiving The Response
In the right-hand pane, you can see the API's response as JSON!

![](./img/insomnia_layout8.png)

---
---

### 3.5 - 📨 Creating A POST Request 📨
The request we just made was a GET request - asking the API to give us some information. Let's adjust it to make a POST request instead, so that we can send new data through to the back-end to be stored. We'll create a new user account.

---

#### 3.5.1 - A Different Request URL
Since we are sending a different type of request, we need to send it to a different endpoint. Here's the new value:

```
https://solitary-glitter-2281.fly.dev/users/
```

---

#### 3.5.2 - A Different REST Verb
Next, we need to click the `GET` dropdown and select `POST` instead:

![](./img/insomnia_layout9.png)

---

#### 3.5.3 - Adding JSON Data To The Request Body
Now we need to supply some data. Click the `Body` dropdown and select `JSON`:

![](./img/insomnia_layout10.png)

Now click in the middle/left pane and define some JSON data to send through with your POST request. We need a `username`, an `email`, and a `password`. You should pick your own values, because the API needs each user account to be unique. Here's what mine looks like:

```JSON
{
	"username": "Ollie1",
	"password": "somepassIguess2",
	"email": "oliver1@lavers.com"
}
```
> You need to use an email address that at least looks like a real value. The one I've used here is fine, but `"xyz"` won't work. The API checks that the format of the address is correct!

---

#### 3.5.4 - Receiving The Response
Now press `Send` again! The API responds with the ID (primary key) of our new user account, plus confirmation of our username and email address!

![](./img/insomnia_outcome.png)

Through the rest of the course, we'll use this tool to interact with our APIs!

<h1><img src=../../global_images/logo.png width="100" />📦 Python Dependency Management 📦<img src=../../global_images/logo.png width="100" /></h1>

Since we are going to start using modules and libraries made by other people to supercharge Python, we need to start thinking about how we are going to manage those extra tools. Because our code depends on these "third-party" modules to run, we call them "**dependencies**".

---
---
---

<h2>Table Of Contents</h2>

- [1 - 🤔 Why Do We Need To Manage Our Dependencies? 🤔](#1----why-do-we-need-to-manage-our-dependencies-)
- [2 - ❓ What's The Solution? ❓](#2----whats-the-solution-)
- [3 - 🛠️ How To Use `venv` 🛠️](#3---️-how-to-use-venv-️)
  - [✅ 3.1 - Making Sure You Have `pip` ✅](#-31---making-sure-you-have-pip-)
    - [3.1a - What To Do If You Don't Have `pip`](#31a---what-to-do-if-you-dont-have-pip)
  - [3.2 - 🪟 A Tweak For Windows 🪟](#32----a-tweak-for-windows-)
  - [3.3 - 🎬 Initialise Git As Usual 🎬](#33----initialise-git-as-usual-)
  - [3.4 - 🏗️ Setting Up Our Virtual Environment 🏗️](#34---️-setting-up-our-virtual-environment-️)
    - [3.4.1 - Creating A `requirements.txt` File](#341---creating-a-requirementstxt-file)
    - [3.4.2 - Creating A `.gitignore` File](#342---creating-a-gitignore-file)
  - [3.5 - 🚦 Activating The Virtual Environment 🚦](#35----activating-the-virtual-environment-)
  - [3.6 - 📥 Installing Requirements 📥](#36----installing-requirements-)
  - [3.7 - 🏍️ Using The Virtual Environment 🏍️](#37---️-using-the-virtual-environment-️)
  - [Ω - 🛑 Turning The Virtual Environment Off When You're Done 🛑](#ω----turning-the-virtual-environment-off-when-youre-done-)

---
---
---

## 1 - 🤔 Why Do We Need To Manage Our Dependencies? 🤔
There are a few considerations at play here:
- When our code is complete, we want to be able to share it with other programmers, so they'll need to know what extra modules are required to make it go.
- We might end up working on our code in a team, so we need to make sure that everyone is using the same version of these third-party tools.
- The libraries we use for this project might later end up getting updated in a way that changes how they work. We need to keep track of what version of these libraries we were using, so that we don't break our code by installing the new versions by mistake.
- The next coding project we start work on will have different dependencies. If we just install every dependency for every project on our computer without any oversight, we'll quickly lose track of which modules serve which projects. And worse - we might get into conflicts where we need version 1 of some library for one project, but we need version 2 of *the same* library for another project! Yikes, what a mess.

---
---
---

## 2 - ❓ What's The Solution? ❓
No matter what language we are working in, the solution is to have some file that contains a list of all the dependencies for our project. Then, we fence off a little section of our computer to act as a "sandbox", and just install the listed dependencies inside the fence. 

In Python we use a tool called `pip` to manage packages. It lets us download and install any library we want from the global shared package index at https://pypi.org/.

The "sandboxing" tool we use for Python is called a "**virtual environment**". There are a few different options, but in this lesson we will be using one called `venv`. You might run into mentors who use different ones - that's ok, they're all pretty similar.

So, our system is going to be this:
- For each project we start, we'll create a virtual environment inside the project folder.
- We will also create a file called `requirements.txt`. We'll fill this file with a list of the dependencies we need for our project.
- Whenever we run our code or install our dependencies, we will first make sure that our virtual environment is turned on. That ensures that our installations are happening inside the sandbox, and our code has access to the libraries it needs.
- Finally, we **won't** back up our virtual environment on Github. (It's quite large, and it only gets bigger as we install more libraries.) Instead we'll tell Git to ignore it. If we ever need to re-create it, we can use the `requirements.txt` file to remember what was in it.

---
---
---

## 3 - 🛠️ How To Use `venv` 🛠️

Let's make it happen! 

The following steps walk you through using the `venv` module to manage your dependencies in Python.

---
---

### ✅ 3.1 - Making Sure You Have `pip` ✅
> [!NOTE]  
> You should only need to do this step once! After this lesson, it'll be sorted.

There are good odds you already have `pip` included in your Python installation. To check, you can run this command in the terminal:

```bash
python -m pip --version
```

> [!IMPORTANT]  
> Remember: your installation might use a different name for `python`, like `python3` or `py`!

You should see something like this:
![](./img/pip_check.png)

---

#### 3.1a - What To Do If You Don't Have `pip`
If instead you get a message saying that `pip` isn't installed, you'll need to go get it.

You should be able to do that by running this command:

```bash
python -m ensurepip --upgrade
```

> If you run into any problems here, grab a mentor and ask for help. Common issues are: 
> - Lack of permissions (try running with `sudo` on Mac, or restarting the terminal with administrator permission on Windows)
> - In some unusual situations, a Python installation might not include the `ensurepip` module. In that case, check out this site for more info: https://pip.pypa.io/en/stable/installation/

---
---

### 3.2 - 🪟 A Tweak For Windows 🪟

> [!NOTE]  
> You should only need to do this step once. After this lesson, it'll be sorted.

> [!IMPORTANT]  
> Only execute this step if you are using a Windows machine! It's not necessary on a Mac.

In rare cases, Windows fails to play nicely with virtual environments. We are going to nip that in the bud.

Search for Powershell in the start menu. Open a new Powershell window **as an administrator**:

![](./img/powershell_admin.png)

Run the following command:

```Powershell
Set-Executionpolicy unrestricted
```

Then enter `Y` when prompted. 

---
---

### 3.3 - 🎬 Initialise Git As Usual 🎬
Just like we always do, we want to set this directory up as a Git repo to manage our code. We use the same command as usual:

```Bash
git init
```

---
---

### 3.4 - 🏗️ Setting Up Our Virtual Environment 🏗️
> [!NOTE]  
> You'll need to do this step once for every time you start a new project!

First we'll need to create a new folder to hold our project for today. In the terminal, navigate to wherever you've been storing your various projects for the course, and create a new folder. A good name for this folder might be `django_tutorial`!

Navigate into that folder, and then run these commands in order:

```Bash
python -m venv venv
```

This creates a virtual environment. 

> [!TIP]  
> It might look funny to use `venv venv` in the command - the second `venv` is the name we are giving to our virtual environment. You could call it anything you want, but it's convenient to always call it `venv`, because it means you'll always use the same commands to activate it.

Now open your working directory in VS Code as usual:

```
code .
```

We have some files we need to create now, in order to make sure your dependencies are correctly managed!

In your VS Code window you should just see a folder called `venv`:

![](./img/empty_vs_code.png)

We need to create two new files: 
- One called `requirements.txt`
- One called `.gitignore`

Make sure you don't accidentally put them inside the `venv` folder! They need to be at the top level.

---

#### 3.4.1 - Creating A `requirements.txt` File

Here's what you should put in requirements.txt:

```txt
# requirements.txt

Django==5.1
djangorestframework==3.15.2
```

This is a list of the dependencies we plan to use. We will use this file to install them, and anyone else who wants to clone down our repo from GitHub will be able to do the same!

---

#### 3.4.2 - Creating A `.gitignore` File

A `.gitignore` file tells Git to ignore some files in your repo. 

This is useful because we don't want our `venv` folder to be pushed to GitHub with the rest of our code. If anyone clones our repo down, they should create their own virtual environment!

For the `.gitignore` we are going to use the template recommended by Github - it is designed to automatically prevent Git from backing up a bunch of different pesky files that we should never want to include. You can find it here: https://github.com/github/gitignore/blob/main/Python.gitignore

To copy the whole file, click the button with the little pair of interlinked boxes:

![](./img/gitignore.png)

You can then safely paste the result into your `.gitignore` file.

Don't forget to save both files!

---
---

### 3.5 - 🚦 Activating The Virtual Environment 🚦
> [!NOTE]  
> This step will need to be performed every time you work on a Django project!

Jump back to the terminal, and make sure you're in the folder that contains your `requirements.txt` file.

On Mac, run this command:

```Bash
source venv/bin/activate
```

On Windows, use this:

```Bash
. venv/Scripts/activate
```

You should now see `(venv)` in your terminal prompt. This is to remind you that you are working inside the virtual environment called `venv`!

---
---

### 3.6 - 📥 Installing Requirements 📥
> [!NOTE]  
> You'll need to repeat this step every time you update your `requirements.txt` file!

Let's install Django and DRF!

The command for this is:

```Bash
python -m pip install -r requirements.txt
```

> [!IMPORTANT]  
> Once again, you'll need to be in the directory that contains your `requirements.txt` file when you run this step!

You can check that the installation was successful by running:

```Bash
python -m pip freeze
```

Django and DRF should be listed in the output (maybe alongside a few other miscellaneous libraries that are get installed automatically along side it):

![](./img/freeze.png)

---
---

### 3.7 - 🏍️ Using The Virtual Environment 🏍️
You should now be ready to get coding. I recommend makind an initial Git commit right away, to give yourself a clean slate to return to.

Before you commit, make sure that you aren't commiting your `venv` directory. You can do this by running the command `git status` and checking to see what files Git can see!

---
---

### Ω - 🛑 Turning The Virtual Environment Off When You're Done 🛑
> [!NOTE]  
> You'll need to repeat this step every time you finish working on a Django project for the day!

Turning off the virtual environment is easy. Just run the following command in the terminal:

```Bash
deactivate
```


<h1><img src=../../global_images/logo.png width="100" />Project Setup<img src=../../global_images/logo.png width="100" /></h1>

Django is so helpful that when you start a new project it will create a bunch of useful files for you right away. This project setup content explains how to get Django to do that setup.

We will be building out the bare bones of the project together in class, and then it will be your job to customise it to suit a use-case of your choice!

---
---

<h2>Table of Contents</h2>

- [1 - 🗂️ The Repo 🗂️](#1---️-the-repo-️)
  - [1.1 - 🌱 Create The Repo 🌱](#11----create-the-repo-)
  - [1.2 - 👯 Clone It Down 👯](#12----clone-it-down-)
- [2 - 🏖️ The Venv 🏖️](#2---️-the-venv-️)
  - [2.1 - 🧪 Creating The Venv 🧪](#21----creating-the-venv-)
  - [2.2 - 🌅 Activating The Venv 🌅](#22----activating-the-venv-)
  - [2.3 - 📦 Installing Dependencies 📦](#23----installing-dependencies-)
- [3 - 🌿 Initialisation 🌿](#3----initialisation-)
  - [3.1 - 🚦 Starting The Project 🚦](#31----starting-the-project-)
  - [3.2 - 🎬 The First App 🎬](#32----the-first-app-)
- [4 - 🗺️ Quick Exploration Break 🗺️](#4---️-quick-exploration-break-️)
  - [4.1 - 🗃️ The Outer Repo 🗃️](#41---️-the-outer-repo-️)
  - [4.2 - 🗂️ The Django Project Directory 🗂️](#42---️-the-django-project-directory-️)
  - [4.3 - 📁 The App Directory 📁](#43----the-app-directory-)
  - [4.4 - 🔩 The Projectwide Settings Directory 🔩](#44----the-projectwide-settings-directory-)
- [5 - ⚙️ Update The Settings ⚙️](#5---️-update-the-settings-️)
- [6 - ➡️ Apply Migrations ➡️](#6---️-apply-migrations-️)
- [7 - 🚀 Look At It Go! 🚀](#7----look-at-it-go-)
- [8 - ⏫ Commit and Push! ⏫](#8----commit-and-push-)

---
---

## 1 - 🗂️ The Repo 🗂️
As usual, we need to create a repository for our project. 

---

### 1.1 - 🌱 Create The Repo 🌱
Let's make one on Github. Here's a screenshot:

![img/1.1.png](./img/1.1.png)

> [!IMPORTANT]  
> Note that I have selected the option to add a README file, and under `Add .gitignore` I have searched for Python to select the Python project template. This is a little quality-of-life tweak!

---

### 1.2 - 👯 Clone It Down 👯
Clone the repo down to a useful location on your local machine. You'll need to grab the URL from Github, and then run the terminal command from your chosen directory location: 

![img/1.2.png](./img/1.2.png)

Hopefully by now the command to clone a repo is getting familiar:

```bash
git clone <your_link_here>
```

> [!NOTE]  
> I've called my repo `crowdfunding_back_end` - that's a good name, because later in the course we'll be creating a front end as well!

---
---

## 2 - 🏖️ The Venv 🏖️
We need to set this repo up with a virtual environment, to turn it into a sandbox where we can install and manage the dependencies that we need.

---

### 2.1 - 🧪 Creating The Venv 🧪
Create a virtual environment:

```bash
python -m venv venv
```

---

### 2.2 - 🌅 Activating The Venv 🌅
And activate it:

```bash
# Windows command

. venv/Scripts/activate
```

```bash
# Mac command

source venv/bin/activate
```

> [!NOTE]  
> There's no need to add your virtual environment to your `.gitignore` this time, as long as you called it `venv`. That's because Github `.gitignore` template that we used contains this default name already. If you chose some other name, you'll need to manually add it.

---

### 2.3 - 📦 Installing Dependencies 📦
Open the repo in VS Code:

```bash
code .
```

Create a `requirements.txt` file next to your `README.md` file:

![img/2.3.png](./img/2.3.png)

Add the following contents to it:

```txt
Django==5.1
djangorestframework==3.15.2
```

And jump back to the terminal to install those requirements:

```bash
pip install -r requirements.txt
```
> [!IMPORTANT]  
> Remember, you **must** have your virtual environment turned on when you run this command!

---
---

## 3 - 🌿 Initialisation 🌿
Initialisation is the process of telling Django to set up a new back-end for us!

---

### 3.1 - 🚦 Starting The Project 🚦
Initialise the Django project with the following command in the terminal:

```bash
django-admin startproject crowdfunding
```

---

### 3.2 - 🎬 The First App 🎬
Django projects are divided into multiple "apps". Each app should handle a chunk of your back-end's functionality. Users will be handled by one app, crowdfunding projects by another, etc.

Now we can create the first app. We'll start by creating an app to manage the various crowdfunding projects that our users create. 

Run the following commands to create a new app:

1.  ```bash
    cd crowdfunding
    ```
    > Navigating into your Django project directory, which is where the files for this app will live.

2.  ```bash
    python manage.py startapp projects
    ```
    > Telling Django to generate the files for our app.

3.  ```bash
    cd ..
    ```
    > Navigating back up a level to the outer repo again.


---
---

## 4 - 🗺️ Quick Exploration Break 🗺️
Let's take a look at the files that Django auto-created for us...

---

### 4.1 - 🗃️ The Outer Repo 🗃️ 

I.e., the `crowdfunding_back_end/` directory!

![4.1](./img/4.1.png)

This is the outermost level of our project directory. It contains:
- the Django project directory (`crowdfunding/`). This is where all your back-end code will live.
- the `venv/` that we just created. 
- the `.gitignore` file, which tells Git which files it shouldn't back up.
- the `README.md` file, that will eventually hold our your notes about the project.
- the `requirements.txt`, which lists our dependencies (Just Django and DRF for now).

---

### 4.2 - 🗂️ The Django Project Directory 🗂️ 

I.e., the `crowdfunding_back_end/crowdfunding/` directory!

![4.2](./img/4.2.png)

This is the Django project directory. It contains:
- The `projects/` app directory.
- A *second* directory called `crowdfunding/`. 
  > This inner `crowdfunding/` folder is just here to contain files that govern the whole project, and don't belong to any one app. (The Django devs could have chosen to just make it so that these files were stored loose in the project directory, but they would add to the clutter.)
- The `manage.py` script. This is a very important file - it lets us interact with the project through the command line. 

---

### 4.3 - 📁 The App Directory 📁 

I.e., the `crowdfunding_back_end/crowdfunding/projects/` directory!

![4.3](./img/4.3.png)

This directory is here to hold code that is specific to "crowdfunding project" functionality on our website. Most websites do multiple things. For example - ours will manage both users *and* crowdfunding projects. 

It makes sense to keep these chunks of functionality separate, so we break them off into their own "apps". Each app gets a folder. 

Important files here are:
- The `migrations/` directory. 
  > Every app directory will have one of these. Migrations are how Django handles changes to the database, so every time you make a new model or change an old one, we'll create a new migration in this directory to track how the database has evolved.
- The `models.py` file.
  > This is where we will define our code for some of our models!
- The `views.py` file.
  > This is where some of our views will live!

---

### 4.4 - 🔩 The Projectwide Settings Directory 🔩 

I.e., the `crowdfunding_back_end/crowdfunding/crowdfunding/` directory!

![4.4](./img/4.4.png)

Like we said, this one contains files that organise the whole project! Important files here are:

- The `settings.py` file.
  > This is where we keep important settings for our back-end.
- The `urls.py` file.
  > Each different type of request that our API serves needs to have its own "endpoint" - an address to which those requests can be sent. We'll define those endpoints by giving each their own URL, organised through in this file.

---

> [!NOTE]
> Wow, there's a lot going on there. Your lead mentor will give you a tour during class, so feel free to ask any questions you might have about this structure. :) 
>
> Even though that one `python -m django startproject` command created a whole bunch of files for us, we still have some work to do to turn this into a working website!
>
> Let's get started on that now.

---
---

## 5 - ⚙️ Update The Settings ⚙️

We've already done some customisation of this project. 
- We installed Django Rest Framework 
- We added our `Projects` app

Any customisation we do needs to be referenced in the project-wide settings file, so that Django knows about it. 

Head over to `crowdfunding_back_end/crowdfunding/crowdfunding/settings.py`. 

![5](./img/5.png)

There's a lot of code in this file, but we only need to make a small change. 

```diff
# ...

INSTALLED_APPS = [
+   'projects.apps.ProjectsConfig',
+   'rest_framework',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

# ...
```

> [!NOTE]  
> You may need to scroll to find the `INSTALLED_APPS` variable.

---
---

## 6 - ➡️ Apply Migrations ➡️

A migration is "a recorded change to a database". 

Since this is the very beginning of our project, Django hasn't set up the databse for us yet. We need to tell it to apply some migrations to make that happen. 

Run the following two commands in the terminal:

```bash
python crowdfunding/manage.py makemigrations
```

```bash
python crowdfunding/manage.py migrate
```

Here's what that looks like in my terminal:

![6](./img/6.png)

> [!NOTE]  
> Since we haven't written any models yet, we are only applying the initial setup migrations here. These are the same every time, and come pre-loaded with Django. 
> 
> That means we could technically have skipped the `makemigrations` step. We just included it so that you'll know the command for later!

If you check your VS Code window you'll notice that there's now a file called `db.sqlite3` in your `crowdfunding/` directory. This is the database that Django just created!

If you install [this VS Code extension](https://marketplace.visualstudio.com/items?itemName=qwtel.sqlite-viewer), you can check out the tables that Django created for us. (There's nothing there that we need to look at in depth yet.)

![6.1](./img/6.1.png)

---
---

## 7 - 🚀 Look At It Go! 🚀

To turn our back-end on, we just run the following command in the terminal:

```bash
python crowdfunding/manage.py runserver
```

Here's what you should see:

![7](./img/7.png)

Navigate to the following address in your browser to check that it worked: [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

You should see the following webpage:

![The Django success screen](./img/launch.png)

> [!IMPORTANT]  
> Keep in mind, the web-page you see here is just for us developers to look at!
>
> Django makes this available to us so that we can check that we have got our site set up correctly. It's not intended for users to ever see - they'll be looking at the front-end that we code up in the next unit.

---
---

## 8 - ⏫ Commit and Push! ⏫

Don't forget to back your work up with Git!

```bash
git status
```

![8](./img/8.png)

> [!IMPORTANT]  
> Make sure you're not committing your `venv/` directory! If you see `venv/` here, you need to make check the contents of your `.gitignore` file.

```bash
git add .
```

```bash
git commit -m "project set up"
```

```bash
git push origin main
```

<h1><img src=../../global_images/logo.png width="100" />💃 Django Models 🕺<img src=../../global_images/logo.png width="100" /></h1>

In this block of content you'll learn to create "models" in Django to manage the data in your database. Let's jump in!

---
---

<h2>Table Of Contents</h2>

- [1 - 🗃️ The Django ORM 🗃️](#1---️-the-django-orm-️)
- [2 - 🛠️ Getting Ready To Code 🛠️](#2---️-getting-ready-to-code-️)
- [3 - 🏗️ Creating Our First Model 🏗️](#3---️-creating-our-first-model-️)
  - [3.1 - 🧐 What Did We Just Write? 🧐](#31----what-did-we-just-write-)
- [4 - ➡️ Time To Migrate Again ➡️](#4---️-time-to-migrate-again-️)
  - [4.1 - 🕵️‍♀️ What Did That Do? 🕵️‍♀️](#41---️️-what-did-that-do-️️)
- [5 - 🐚 The Django Shell 🐚](#5----the-django-shell-)
  - [5.1 - 🌱 Creating A Model Instance 🌱](#51----creating-a-model-instance-)
  - [5.2 - ⬅️ Retrieving Records In The Shell ⬅️](#52---️-retrieving-records-in-the-shell-️)
- [6 - ⏫ Commit And Push! ⏫](#6----commit-and-push-)

---
---

## 1 - 🗃️ The Django ORM 🗃️

An Object-Relational Mapper (ORM) is a programming technique used to convert data between incompatible systems (in this case, between Python objects and database tables). 

Django’s ORM allows us to manipulate database data using Python classes and methods. This means that we don't have to mess around writing complex SQL queries when we get data from our database!

The classes we create will be our "models". We will create them by "inheriting" from Django's built-in classes. These come bundled with a bunch of useful functionality. That means that the only "original" coding we will need to do will be to tell Django what data we want our app to manage, and how it should manage that data.

---
---

## 2 - 🛠️ Getting Ready To Code 🛠️

Open the terminal, and navigate to your crowdfunding project. For me, that looks like this:

```bash
cd she_codes/crowdfunding_back_end/
```

> [!NOTE]  
> Your command might looks slightly different depending on where you placed your project directory. Use `ls` and `cd` to navigate around as required!

Now turn on your `venv`. Remember, the commands for Windows and Mac are slightly different:

```bash
# Windows command:
. venv/Scripts/activate
```

```bash
# Mac command:
source venv/bin/activate
```

Open VS Code:

```bash
code .
```

Ok, let's get coding!

---
---

## 3 - 🏗️ Creating Our First Model 🏗️

The code we need to write goes in the `crowdfunding_back_end/crowdfunding/projects/models.py` file:

![3](./img/3.png)

Here are the changes to make:

```diff
from django.db import models

- # Create your models here.
+ class Project(models.Model):
+   title = models.CharField(max_length=200)
+   description = models.TextField()
+   goal = models.IntegerField()
+   image = models.URLField()
+   is_open = models.BooleanField()
+   date_created = models.DateTimeField(auto_now_add=True)
```

> [!NOTE]  
> Make sure you get your indentation correct! We recommend that you type this code out, rather than copy-pasting it.

---

### 3.1 - 🧐 What Did We Just Write? 🧐

What we've created here is a Python class definition. There are only a few of special things to note about it:

- We inherited our class from the built-in `models.Model` class that comes with Django. This means that our new model has a bunch of incredibly useful functionality right out of the box. Django will even create a database table for us based on this model!
- Our model has a bunch of attributes: `title`, `description`, etc. Each of these is itself an instance of one of the classes that comes bundled with Django. These attributes tell Django what types of fields we want in our database table.
- We can pass arguments to our model's field attributes to specify extra functionality. Here we've said that the `title` field cannot be more than 200 characters long, and that the `date_created` field should be automatically set with the current date when a new record is created.

In plain English, we have basically told Django this...
> *"Hey, make me a table in the database called `Project`, and give it the following columns:*
> - *title - this field should contain short strings of characters*
> - *description - this field should contain longer blocks of text*
> - *goal - this field should contain an integer*
> - *etc...*

---
---

## 4 - ➡️ Time To Migrate Again ➡️

Any time we make a change to a model, we need to make a new database migration. This tells Django to update the database tables to match.

Jump into the terminal, check you are in the `crowdfunding_back_end/` directory with your `venv` activated, and run the following commands:

```bash
python crowdfunding/manage.py makemigrations
```

```bash
python crowdfunding/manage.py migrate
```

![4](./img/4.png)

> [!NOTE]  
> Notice that since we actually made a change to a model this time, running `makemigrations` actually does something!
>
> If you're feeling curious, check out the `crowdfunding/projects/migrations/0001_initial.py` file that was created.

---

### 4.1 - 🕵️‍♀️ What Did That Do? 🕵️‍♀️

If you have [the SQLite Viewer extension for VS Code](https://marketplace.visualstudio.com/items?itemName=qwtel.sqlite-viewer) installed, you can take a look at your database tables. 

Can you see the table we just created?

![4.1](./img/4.1.png)

There's nothing in this table yet, of course. But we can use our new model to put some things there!

---
---

## 5 - 🐚 The Django Shell 🐚

We can't use Insomnia to send data to our back-end yet, since we haven't written any views or serializers. Luckily, Django comes with a command line tool that will let us give our new model a test drive anyway.

Jump into the terminal, and run the following command:

```bash
python crowdfunding/manage.py shell
```

This opens a shell program that lets us interact with our Django back-end directly.

![5](./img/5.png)

---

### 5.1 - 🌱 Creating A Model Instance 🌱

Let's give the Django shell some commands!

Run the following commands in order:

1.  ```python
    from projects.models import Project
    ```
1.  ```python
    first_record = Project()
    ```
1.  ```python
    first_record.title = "Test Project"
    ```
1.  ```python
    first_record.description = "A test crowdfunding project"
    ```
1.  ```python
    first_record.goal = 9001
    ```
1.  ```python
    first_record.image = "https://upload.wikimedia.org/wikipedia/commons/thumb/4/48/Silly_Dog_%282277051513%29.jpg/320px-Silly_Dog_%282277051513%29.jpg"
    ```
    > It's ok to copy-paste that address!
1.  ```python
    first_record.is_open = True
    ```
1.  ```python
    first_record.save()
    ```
1.  ```python
    exit()
    ```

Hopefully you can see what's happening here. We've issued Python commands to create an instance of the `Project` class that is our model. Then we've set a value for each field of that class instance, and finally saved the instance as a record in our database.

We can even see the new row that has been created in our database table!

![5.1](./img/5.1.png)

---

### 5.2 - ⬅️ Retrieving Records In The Shell ⬅️

We just used our model to create a record in the database, but we can also use it to retrieve records from the database. 

Let's open the shell again:

```bash
python crowdfunding/manage.py shell
```

Now run these commands in order:

1.  ```python
    from projects.models import Project
    ```
1.  ```python
    projects_list = Project.objects.all()
    ```
1.  ```python
    print(projects_list)
    ```

![5.2](./img/5.2.png)

The `.objects` field is build into every Django model. It lets us manage records in the database. 

Here we have run the `Project.objects.all()` method. This gets us a "queryset" object that contains every single record in the `Project` table.

Since our `first_record` instance is the only row in the table, it is the first and only result in the queryset. Let's take a look at it:

1.  ```python
    first_record = projects_list[0]
    ```
1.  ```python
    print(first_record.title)
    ```

![5.2.1](./img/5.2.1.png)

Looking good! Our record was successfully retrieved from the database table!

Don't forget to exit the shell!

```python
exit()
```

---
---

## 6 - ⏫ Commit And Push! ⏫

Don't forget to commit your changes! Remember those commands?

1.  ```bash
    git status
    ```
1.  ```bash
    git add .
    ```
1.  ```bash
    git commit -m "wrote our first django model"
    ```
1.  ```bash
    git push origin main
    ```