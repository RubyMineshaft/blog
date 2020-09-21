---
layout: post
title:      "Forms Posting to an Incorrect Route"
date:       2018-10-30 03:02:14 -0400
permalink:  forms_posting_to_an_incorrect_route
---


This week I've been working on my Sinatra portfolio project for [Flatiron School](http://flatironschool.com).  Today I ran into an issue where a form was posting to an incorrect route.  I spent a good three or four hours trying to figure out what was wrong, so I thought I would share this in hopes that maybe one day it will save someone a few hours of digging. 

First, let's take a look at the specific issue that was plaguing me.  This is the particular section of code I was having trouble getting to work:

        <% @dream.comments.each do |comment| %>
          <div class="card">
            <div class="card-header">
              <span><%= comment.user.username %></span>
              <span id="comment-date" class="date"><%= comment.created_at %></span>
            </div>
            <p class="card-text pad"><%= comment.content %></p>
            <% if comment.user == current_user %>
              <a href="/comments/<%= comment.id %>/edit">Edit Comment</a>
              <form action="/comments/<%= comment.id %>" method="post">
                <input type="hidden" name="_method" value="delete">
                <input type="submit" value="Delete">
              </form>
            <% end %>
                    
This section comes from an ERB file, or Embedded Ruby, which is basically a file that allows you to include Ruby code inside your HTML.  In this section, we are iterating over an array of comments and passing each into a block variable `comment`. We then go on to display all of the information about each individual comment.  Finally, when we get to `<% if comment.user == current_user %>`, we check to see if the user viewing the page is the same user who posted the comment. If so, we give the user a link to edit his/her comment along with a button provided from a form to delete it. Looks good so far, right? 

Let's take a closer look at that form: `<form action="/comments/<%= comment.id %>" method="post">` When the user submits the form it should be sent via an HTTP POST request to `/comments/:id` :id being whatever the id of the comment is.  `<input type="hidden" name="_method" value="delete">` This line uses the `Rack::MethodOverride` middleware via a hidden input to perform a DELETE request, since HTML forms only support GET and POST.  Finally, we have our delete button: `<input type="submit" value="Delete">`. 

This form looks absolutely fine. It should work without any problems, provided I have my routes set up properly in my controllers. However, it didn't work.  

<p align="center"><img src="https://i.imgur.com/BKURbXv.png"></p>

The form was sending the DELETE request to `/comments` instead of `/comments/5` or whichever id number it needed to for a particular comment.  What gives?

<p align="center"><img src="https://media.giphy.com/media/U6aAKnv1z4brq/giphy.gif"></p>

After several hours of trying to figure out what was going on and posting questions in the flatiron slack channels and on stack overflow, a friend helped me take a look at my code to see if he could figure out where the error was occurring.  

After looking through into the issue for a while, he noticed that in the developer console there was no form tag around my delete button when there clearly was one in my ERB file.  This led us to believe that the issue was some sort of Javascript element.  After a few more minutes of digging, I noticed something a little higher up on the page. 

       <form action="/comments" method="post">
          <h5><label for="comment_input">Add a comment:</label></h5>
          <div class="input-group mb-3">
            <input type="text" class="form-control" name="comment[content]" placeholder="Enter your comment" aria-label="Comment" aria-describedby="button-addon2">
            <div class="input-group-append">
              <input type="hidden" name="comment[dream_id]" value="<%= @dream.id %>">
              <button class="btn btn-outline-secondary" type="submit" id="button-addon2">Save Comment</button>
            </div>
          </div>
                    
This form, which posts to `/comments` **doesn't have a closing tag**! The browser was basically interpreting everything as one big form! Who would think that something as simple as a missing `</form>` would cause so much trouble? 

<p align="center"><img src="https://media.giphy.com/media/vX9WcCiWwUF7G/giphy.gif"></p>

Honestly, this was a very simple mistake and something that should not have taken four hours to find. Moral of the story here is go ahead and close your tags when you open them. It saves you a lot of energy if you happen to forget. 

And if your form isn't going where you want it to go, **check the other forms on the page**!





