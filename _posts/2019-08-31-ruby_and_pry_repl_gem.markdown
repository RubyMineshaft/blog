---
layout: post
title:      "Ruby and Pry REPL Gem"
date:       2019-08-31 23:23:00 +0000
permalink:  ruby_and_pry_repl_gem
---


Pry is an REPL Gem that offers a ton of useful features over IRB. 

With Pry we are able to jump into the context of our code which is extremely useful for debugging. 

To get started using Pry you can install it with `gem install pry` or add it to your Gemfile:

```
gem "pry"
```

The next step in using Pry with your project is to require it:

```
require 'pry'
```

Now that you have required pry, it's very easy to debug.  To debug using pry you simply add a `binding.pry` in your code.  When executing your code, Ruby will freeze whenever it hits the binding and allow you to test methods and variables. 
It's so much easier to figure out what is wrong with your code when you are able to jump straight into the context. 
