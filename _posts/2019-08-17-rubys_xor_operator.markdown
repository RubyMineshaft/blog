---
layout: post
title:      "Ruby's ^ XOR Operator"
date:       2019-08-17 15:32:48 -0400
permalink:  rubys_xor_operator
---


Ruby's ^ operator is a nifty operator to use if you need to test whether one (and only one) of the inputs are true.

```ruby
true ^ false 
# => true

true ^ true
# => false

false ^ false
# => false
```

As we can see in this example, inputs of true and false return a true value, where two true inputs return false.

Since each ^ operator is evaluated individually we could even do something like this:

```ruby
true ^ true ^ false ^ true ^ false
```

What would something like this return? An odd number of `true` values would return `true`, and an even number will return `false`. Each `^` is evaluated in order, so our first evaluation of `true ^ true` would return `false`. So now we have:

```ruby
false ^ false ^ true ^ false
```

`false ^ false` returns `false`:

```ruby 
false ^ true ^ false
```

`false ^ true` returns `true`:

```ruby
true ^ false
```

And finally  as we know `true ^ false` returns `true`.

