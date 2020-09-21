---
layout: post
title:      "Using the Bootstrap_form Gem with Rails"
date:       2019-04-09 02:10:56 -0400
permalink:  using_the_bootstrap_form_gem_with_rails
---


For the past few weeks I have been working on my Rails portfolio project for Flatiron School.  I decided to make an app for sharing Art events. 

I decided to use Bootstrap to make it look a bit better (I am in no shape or form a designer).  Manually adding all of the classes to forms in rails for bootstrap is a lot of work.  Luckily, there is a beautiful little Gem called bootstrap_form that works with the Rails `form_for`, `form_with`, and `form_tag` helpers. 

It's very simple to use.  You simply replace `form_for` with `bootstrap_form_for` and the gem does all the heavy lifting for you. 

An example from my app: 

```
<%= bootstrap_form_for([@user, @artwork]) do |f| %>

  <%= f.text_field :title %>

  <%= f.date_field :date %>

  <%= f.text_area :description %>

  <%= f.text_field :url, placeholder: "http://example.com/"%>

  <%= f.file_field :images, :multiple => true %>

  <%= f.submit %>

<% end %>
```

This form is for a nested resource, but it works just as well with non-nested resources.  The output of the code above is:

```
<form class="new_artwork" id="new_artwork" role="form" enctype="multipart/form-data" action="/users/1/artworks" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="✓"><input type="hidden" name="authenticity_token" value="/mXSgjL/RfXs+qMbhp4uzKFZSJ8XOrY2pGk30Eb+nmynXuET1pHhTVnDuZuYxJRgue1VEiGIJI3Tis+QLtXISg==">

  <div class="form-group"><label class="required" for="artwork_title">Title</label><input class="form-control" type="text" name="artwork[title]" id="artwork_title"></div>

  <div class="form-group"><label class="required" for="artwork_date">Date</label><input class="form-control" type="date" name="artwork[date]" id="artwork_date"></div>

  <div class="form-group"><label class="required" for="artwork_description">Description</label><textarea class="form-control" name="artwork[description]" id="artwork_description"></textarea></div>

  <div class="form-group"><label for="artwork_url">Url</label><input placeholder="http://example.com/" class="form-control" type="text" name="artwork[url]" id="artwork_url"></div>

  <div class="form-group"><label for="artwork_images">Images</label><div class="custom-file"><input multiple="multiple" class="custom-file-input" type="file" name="artwork[images][]" id="artwork_images"><label class="custom-file-label" for="artwork_images">Choose file</label></div></div>

  <input type="submit" name="commit" value="Create Artwork" class="btn btn-secondary" data-disable-with="Create Artwork">

</form>
```

`bootstrap_form_tag` works a little bit differently than `form_tag`.  It's very similary to how `form_for` works.  You simply pass it a hash with a key of url as an argument and it takes a block. 

```
<%= bootstrap_form_tag url: "/login" do |f| %>
  <%= f.email_field :email %>

  <%= f.password_field :password %>

  <%= f.submit "Log In" %>
<% end %>
```

It's easy to see how this could save you a lot of time if you are using Bootstrap in your Rails app. For more information on the bootstrap_form gem you can read its full documentation here: [Bootstrap_form](https://github.com/bootstrap-ruby/bootstrap_form) 




