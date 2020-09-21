---
layout: post
title:      "DreamCatcher Sinatra App"
date:       2018-11-03 22:01:51 +0000
permalink:  dreamcatcher_sinatra_app
---


I created a dream journal app for my Flatiron Sinatra portfolio project.  The app allows users to create an account, log in, and keep a record of their dreams. Users have the option of sharing dreams publicly or keeping them private.  

The first step after deciding what I wanted to make was figuring out what models I wanted to include. I decided I'd like to have users, dreams, categories, and comments.  Since categories and dreams have a many to many relationship, I also needed a dream_categories join table and a corresponding class in the models.  after everything was set up my schema looked like this: 

```
ActiveRecord::Schema.define(version: 2018_10_28_075912) do

  create_table "categories", force: :cascade do |t|
    t.string "name"
  end

  create_table "comments", force: :cascade do |t|
    t.text "content"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.integer "user_id"
    t.integer "dream_id"
  end

  create_table "dream_categories", force: :cascade do |t|
    t.integer "dream_id"
    t.integer "category_id"
  end

  create_table "dreams", force: :cascade do |t|
    t.string "title"
    t.text "content"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.integer "user_id"
    t.boolean "private", default: false
  end

  create_table "users", force: :cascade do |t|
    t.string "username"
    t.string "password_digest"
    t.string "email"
    t.string "city"
    t.text "bio"
  end

end
```

Now that the models and database were set up, it was time to get to work on my controllers and views.  I decided to have controllers that handle actions specifically for each class. This meant having application, users, dreams, categories, and comments controllers.

I decided to style my views using Twitter Bootstrap.  If there is one thing that I have learned while working on this project, it is that I much prefer working with back-end technologies to working with css. It's not that I find styling; it's just not as exciting as working with ruby.  

When all was said and done my landing page came out looking like this:

![](https://i.imgur.com/V0QhzOm.png)

Overall, everything went pretty smoothly during this project. I found it to be pretty easy.  I did, however, have one hiccup that wasted a bit of time, which you can read about in [this post](http://mattetress.com/forms_posting_to_an_incorrect_route).   I'm submitting my project today and can't wait to see what is in store next!

If you'd like to see more about this project you can play around with the [heroku deployment](http://dreamcatcher-sinatra.herokuapp.com).  For a closer look at the code, take a look at this project's [GitHub repository](https://github.com/mattetress/dreamcatcher-sinatra-app).


