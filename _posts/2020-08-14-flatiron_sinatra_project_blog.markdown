---
layout: post
title:      "Flatiron Sinatra Project Blog"
date:       2020-08-14 15:08:33 +0000
permalink:  flatiron_sinatra_project_blog
---


So the original concept for this related to a position I had been interviewing for. I knew that the company had a system for tracking vehicles and wanted to build the beginnings of a more useful tracking system that could be expanded to data collection and analysis. In a sense I was starting from a slightly different position because Ideally another system would be responsible for creating the data. For the purposes of this project I mostly abandoned this idea.

I used the corneal gem to get the framework set up. To use you simply navigate to the location on your machine you wish the files to be located in your terminal and the run 'corneal new "project name". This creates most of the files and folders that you might need. 

I started by setting up the databases using rake and rake seed. I was able to use faker for some of the fields though I needed to use .sample for others where faker did not provide the correct information. 

``` ruby
20.times do
station_array =['Wash1','Wash2','PP1','PP2','Bay1','Bay2','Bay3','Bay4','Bay5','Bay6','Bay7','Bay8','Bay9','Bay10','Bay11','Bay12']
location_array = ['Main','Acces','Final']
Location.create(station: "#{station_array[rand(station_array.length)]}", building: "#{location_array.sample}")
end
400.times do
Vehicle.create(vin: Faker::Vehicle.vin, model: Faker::Vehicle.model(make_of_model: 'Toyota'), sub_model: Faker::Vehicle.drive_type, location_id: rand(124..144))
end
20.times do
Modification.create(name: Faker::Vehicle.car_options)
end
```

The main application controllers were next and required that I set up a few helper methods. These would mostly be used to ensure that users who had not logged in would not be able to access any of the site. 

``` ruby 
helpers do
    def logged_in?
      !!current_user
    end
    def current_user
      @current_user ||= User.find_by(id: session[:user_id])
    end
    def redirect_if_logged_out
      redirect to '/' unless logged_in?
    end
  end
```

After this I set up the views and controllers for the user, locations, and vehicles. These all have basic CRUD setup and RESTful structure. 

The last components included verifying that the owner of the vehicle or location would be the only person that could modify the record. The way I accomplished this was firstly  checking that the user was logged in and then checking that the current user was == to the vehicle or location's user_id field in the database. An example is given below:

``` ruby
get '/locations/:id' do 
        redirect_if_logged_out
        @location = Location.find(params[:id])
        redirect_if_unauth_user(@location.user_id)
        erb :'/locations/show'
end
```

Areas that could still be improved as of the time of writing this would include the following:
1. Create New functionality for vehicles and locations (I will likely add even though for this project it might not make logical sense as it is a requirement for the project)
2. Modified CSS for a more attractive appearance
3. Hosting instead of local using 'shotgun'


