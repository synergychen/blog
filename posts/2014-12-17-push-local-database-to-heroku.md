---
title: Push Local Database to Heroku
date: 2014-12-17T18:18:09+00:00
layout: post
categories: Heroku
---

> I spent long time typing data into local database, do I have to do it again in Heroku production database?

### NO

You could clone your local database to Heroku by simply do

{% highlight bash %}
heroku pg:reset DATABASE_URL && heroku pg:push your_app_name_development DATABASE_URL
{% endhighlight %}

`DATABASE_URL` is exactly what it is, you don't need to substitute it with anything else.

Replace `your_app_name_development` with your app information. For example, if your app names **Taskr**, then it should be

{% highlight bash %}
heroku pg:reset DATABASE_URL && heroku pg:push taskr_development DATABASE_URL
{% endhighlight %}

### Notice

It's better to backup Heroku database before pushing local database, since this command would overwrite whole database on Heroku.
