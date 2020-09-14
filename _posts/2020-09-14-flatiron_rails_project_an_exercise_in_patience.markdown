---
layout: post
title:      "Flatiron Rails Project: An Exercise in Patience"
date:       2020-09-14 13:07:12 +0000
permalink:  flatiron_rails_project_an_exercise_in_patience
---


Getting started:
Create your initial rails structure and files by navigating to folder the folder in your terminal and running rails new project_name. Create a new repository on github and follow the instructions to create the first commit.
Set up your resources using: rails g resource resource_name string:column_name string:column_name2
Set up sessions controller files and login/signup views. Set up logout link and routes. 

The Thick of It:
I chose to create an application for tracking and adding courses and notes related to educational pursuits. A common problem I have is seeing a class or lecture that looks interesting, but I just don’t have the time immediately to commit to it. By saving these items in a repository I can come back whenever I have time to try my hand at learning something new. 
I first established the structure of the database by lining out my relationships. I then was able to decide on attributes for each of the tables. With this set, I was able to confirm that I would be able to meet the requirements for the project. 
From this point, things were simply a matter of build then test to make sure things were working as I had intended. The project was largely error driven.

Notes!
When using datetime fields in your database, f.date_select will create a field with a year, month, and day dropdown which will properly save to your database.
I made use of several before actions mainly to redirect if not logged in, set objects, and redirect if attempting to access an object that the user did not own.
Partials within each object view were used for the new and update forms. At the layout level, I created an errors partial that is used by most all of the object views. There are also partials for the nav bar. One for logged in users and one for logged out users.
Migrations on Rails Guide:
https://guides.rubyonrails.org/active_record_migrations.html
Rails Column Types:
https://fullstackheroes.com/rails/column-types/



Errors!
Update/Edit button did not work when pressed. Button press would do nothing. After some googling I found that invalid HTML actually creates this error commonly. In my particular case I had a <div class=kjhdgjh> with no </div>. The page would work properly after reloading the page but would not work on the first attempt after arriving.

TYPE is not an allowable column name in SQL. The migration successfully passed and created the table but any time I tried to persist data to the table I would receive an error. The correction for this is creating a migration to rename the column.

Any time you receive a false return from a .save method it can be useful to drop in a binding and try .save! Instead. This will present you with more information related to why the initial .save failed. 

