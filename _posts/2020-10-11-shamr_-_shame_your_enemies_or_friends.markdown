---
layout: post
title:      "SHAMR - Shame your enemies (or friends)"
date:       2020-10-11 19:24:46 +0000
permalink:  shamr_-_shame_your_enemies_or_friends
---


For this project I wanted to have a bit of fun. I had seen a report on the ‘Chinese’ Social Credit System’ and was reminded how tech can be both a great tool and an instrument for bad actors. In an effort to explore this idea furth I decided to build SHAMR (pronounced SHAME-ER).

The app allows a user to add twitter users to the database and assign those users ‘offenses’. In order to keep things light I chose offenses such as ‘being a slow walker’ or ‘incorrect pronunciation of gif’. A feature that I was not able to implement as of writing this blog was the ‘SHAME’ button. This button should query twitter for a list of all friends associated with the imputed users. If the submitted twitter name was friends with any of the Offenders, they would be provided with a list of ‘offenses’ that they by relation would seem to support.

To start I generated the rails api backend with the --api and --database=postgresql tags
‘rails new apiname --api --database=postgresql’

Set up included some additional steps:
Enable rack cors in gemfile and run bundle
Uncomment lines 8-16 in cors.rb under config/initializers
Change origins to ‘*’ to allow requests from all addresses (or localhost:3000)

Create controllers with RESTful CRUD actions

Create routes in routes.rb file (resources :controller_name)

Create models and migrations with ‘rails g model model_name’
Adjust migrations to include appropriate columns and types

Run ‘rails db:create’ (only necessary with postgreSQL)
Run ‘rails db:migrate’

Create controllers and set to render json
Create serializers

After those steps were complete I set out to start setting up the frontend. I created an ‘assets’ folder where the javascripts folder and index.html files resided. I quickly grabbed a CSS starter theme from the W3 website and modified the head section of the HTML file to reference my javascript.js files. I then tested to make sure everything was interacting correctly. From this point it was a flurry of testing and reworking. As a note, I initially set up my JS files without the use of any classes. Converting the commands to a class and file based structure was beneficial to my understanding of how the code was functioning, though I do not suggest attacking the project in this way.

Issues and Discoveries:
Using an <a> tag you can place an href= attribute with #name_of_another_tag_id. Clicking this link will autoscroll to that portion of the page.
I initially used a toggle hide/show function as show here (https://www.w3schools.com/howto/howto_js_toggle_hide_show.asp) though I found that hat I actually desired was for the user to click a button and only one or the other section would show. This can be seen under the showOffenses and showOffender function in the application.js file.
In order to interpolate a value within a string you must use the ` (back quote) instead of the ‘ (single quotation mark). This broke me for a while.
‘Protected’ is a reserved word in javascript and cannot be used as a column name in your db. See (https://www.w3schools.com/js/js_reserved.asp)




REPO LINK: https://github.com/Soundwood/SHAMR

WALKTHROUGH LINK: https://youtu.be/SJu-Heqd_KQ


