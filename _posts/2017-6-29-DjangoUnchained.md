---
layout: post
title: Django Unchaining (Part-1)
author: Aniket Pandey
---

I got a project under Programming club in summers that turned out to be a great experience in creating a scalable web application in **Django**.
My project partner, Ashish and me started off by building a basic library portal through which it is possible to add users,
authenticate their account, and allow them to borrow books online. 

It does sound cool but it really is very frustrating if you try is by your own the very first time. Our mentor Pratham asked us to 
create this library so that we can be fairly comfortable while starting the main project. I searched for some tutorials on 
Django on the internet, and found one by MDN which coincidentally, was also focused on staring out with a library. 

### Writing my first server

I tried following that tutorial but somewhere in between I got distracted and couldn't complete the portal. I assumed I'll have enough
time to completely grasp the concepts and then work on our main project. But when I came back to campus in mid-May to start off 
the camp, I realized I should've given more time to learning basics as Ashish had already created his portal which looked 
stunning and it already had all the features that Pratham asked us to include.

With no option left, I pulled two all-nighters and tried reading the source code Ashish had written. Though it was tough initially,
I finally started understanding how things worked in Django.

### What is Django

Django is a web-framework written in Python which allows us to create dynamic and scalable web application through which, it is 
easy to manage users of various permissions. Also, Django being in Python makes it more intuitive and easy to understand. I had already 
done a lot of programming in Python while preparing for GSoC (in this blog). So picking up new concepts wasn't that hard.

There are three main components in Django

* Models
* Views
* Templates

#### Models

> A model is the single, definitive source of information about your data. It contains the essential fields and behaviors
 of the data you’re storing. Generally, each model maps to a single database table.

Model is like the brain of your application. It contains the information about all the columns of each table in the database.
 
#### Views

> A view function, or view for short, is simply a Python function that takes a Web request and returns a Web response.
 This response can be the HTML contents of a Web page, or a redirect, or a 404 error.
 
Through views, we can handle requests from clients and return a response afterwards. The response is generally in form of
rendered HTML page or in form of common data like JSON. JSON is extremely useful in creating web APIs through which we can 
let server and client communicate quickly. Also, both can be written in different languages and still work just fine.

#### Templates

>  A template contains the static parts of the desired HTML output as well as some special syntax describing how dynamic 
content will be inserted.

Templates are what let you create user friendly interface. Django has its own template system through which you can write
 python inside of html. 
 
There are a lot of other functionalities offered in django like _forms_, _admin portal_, _user authentication_, _csrf_, etc.
We used a major part of what django had to offer. 

### IITK Authentication

The authentication system in django makes use of the users stored in database. Since we did not have anyone's account pre-
recorded, we had to rely on the fact that once someone logs in, we can ask them to fill the rest of their details like, name,
roll no, address etc. However, there was no way of limiting the users to the IITK junta. Since anybody can log in and pose
as a valid student, we had to override this authentication system. 

Fortunately, django allows us to have our own authentication system, so we wrote it by ourselves, using _new-webmail_'s database,
we were able to identify if someone who is logging in is actually a student of IIT Kanpur. This was the first major step in our project.


