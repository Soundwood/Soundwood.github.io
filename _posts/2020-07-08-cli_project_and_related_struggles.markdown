---
layout: post
title:      "CLI Project and Related Struggles"
date:       2020-07-08 14:58:49 +0000
permalink:  cli_project_and_related_struggles
---


I chose for my project to start on something that I believe I  could grow to a larger project as my skills progressed. The YouTube Music Video search CLI is really not useful as it only replaces the already easily accessible search bar on YouTube’s website. However, in the future it will be easier to locate videos and embed them automatically into a website given a set of criteria. 

In order to keep this short I will focus only on the problems I encountered instead of working through the entirety of the build process.

I was experiencing problems with the search function ‘remembering’ previous searches. Through using the binding.pry command I was able to determine that the ‘.insert’ method I had been using on my YouTube API https address was in fact destructive in that it was permanently modifying the https string. As an example, where I had first inserted ‘%20Bob%20Marley’, the next insert would also include that insert as well as my next search of ‘%20Soundgarden’. The result of the search would be whichever search term was higher ranked from essentially searching for “Bob Marley Soundgarden”. The situation worsened the more times the search command was used before closing the program. The solution was to split the string and concatenate the string back together around the search portion. I could have also just added the search portion to the end of the string since I later discovered that the search modifiers could be in any order.

The code at this point worked as intended but was ugly, repetitive, and did not have single roles for individual classes in the YouTube API and CLI Classes. An additional Video Class was needed to take the search results provided by the YouTube API and provide information related to an individual video. It would also allow for expansion into returning additional results from the API Class if needed at a later date. I created the Video Class to take an argument of the YouTube API Response and a video rank. The Video Class then could return information related to a single video such as the ID and Title.

I had arbitrarily chosen to return the top 3 results for the top music video and live music searches. While the code worked it would be very hard to increase or decrease the number of results. I implemented a small loop which printed the required information to the console a set number of times. Future versions of this program could be modified to request the desired number of results from the user more easily. 

Lastly, after implementing the dotenv Ruby Gem I moved my API keys to the env file and used gitignore to remove the env file from my commits. Unfortunately my previous commits still contained the sensitive information though the repository at the time was still set to private. I googled how to remove this and came upon a series of git commands that essentially created a new branch without the current history, deleted the older master branch, then renamed the new branch back to master. This resolved the issue but resulted in the loss of all previous commit history. Lesson learned. 
In all the project was largely productive in practicing using the local environment and getting more familiar with git. I am glad to be done and enjoyed the process of creating something that is my own even if it is not entirely useful at this point. 

