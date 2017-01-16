---
title: Push Your Rails App to Cloud (Heroku)
date: 2014-10-08T17:06:29+00:00
layout: post
categories: Ruby_on_Rails
---

> Show your ideas with the world!

It's time to push your first rails app to the cloud with Heroku.

Heroku is a cloud platform allowing you to upload your app to their server, so that everyone else on the Internet could access your app. Here as an example, I would demonstrate uploading a Rails app to Heroku.

### Register [Heroku](https://www.heroku.com/) account

### Install Heroku and add ssh keys in local

In OSX or Unix, you could use `brew` to install Heroku.

{% highlight bash %}
brew install heroku
{% endhighlight %}

{% highlight bash %}
heroku login
{% endhighlight %}

{% highlight bash %}
heroku keys:add
{% endhighlight %}

{% highlight bash %}
heroku keys
{% endhighlight %}

### Add essential gem: rails_12factor

This gem is used to make assets in production like JavaScript, css to work properly, and set logger to standard out.

{% highlight ruby %}
gem 'rails_12factor', group: :production
{% endhighlight %}

Install gem using bunlde in command line

{% highlight bash %}
bundle
{% endhighlight %}

Now Heroku infrastructures have been built, let's start to create app on Heroku.

### Create app on Heroku

{% highlight bash %}
heroku apps:create
{% endhighlight %}

### Push you local (master) to Heroku

This is the same as push all your change to github.

{% highlight bash %}
git push heroku master
{% endhighlight %}

### Migrate database on Heroku

Same as migrating locally, we need to run migrate on Heroku server so as to create, edit and delete data on the cloud.

{% highlight bash %}
heroku run rake db:migrate
{% endhighlight %}

### Open your app

Everything is ready, now we could open our app and it would automatically lead us to a new link to Heroku server.

{% highlight bash %}
heroku open
{% endhighlight %}

### See heroku logs

If you want to see the status of the server, and who has done a GET or POST to your website, Heroku logs could easily been reached.

{% highlight bash %}
heroku logs
{% endhighlight %}

### Debug and test app on Heroku

Heroku does provide a rails console to let you access the cloud database for Rails app.

{% highlight bash %}
heroku run rails console
{% endhighlight %}
