---
title: Easy and Fast User Authentication Using Monban
date: 2014-10-13 14:41:13
layout: post
categories: Ruby-On-Rails
---
> Monban makes life easier for user authentication in Rails.

### Why Monban?

Usually when we try to realize user authentication in our app, what we do is

- generate a User model and migration
- add session and users routes
- generate sessions controller (new, create, destroy) and users controller (new, create)
- create sessions and users view (new)
- validates email and password_digest

However, once we use Monban, we can squeeze all the 5 steps, which includes around 100 lines of coding (click [here](https://github.com/tolearn2/shoutr/commit/32de51f486d7f69d72b45c48a95979f2b4b4089c) to see), into 4 commands.

Yes, 100 to 4 lines. That's what Monban does.

### Monban generator

Monban generators is a tool help us to generate and run Monban. Here are the 3 commands

#### 1. Add gem in Gemfile

{% highlight ruby %}
gem 'monban-generators'
{% endhighlight %}

#### 2. Install gem

{% highlight ruby %}
bundle
{% endhighlight %}

#### 3. Generate monban scaffold

{% highlight ruby %}
rails g monban:scaffold
{% endhighlight %}

#### 4. Create and migrate database

{% highlight ruby %}
rake db:create db:migrate
{% endhighlight %}

Go to `http://localhost:3000/users/new` and congratulations!
