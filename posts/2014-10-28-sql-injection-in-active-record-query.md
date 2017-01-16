---
title: SQL Injection in Active Record Query
date: 2014-10-28T17:51:46+00:00
layout: post
categories: Ruby-On-Rails
---

> Find a bug and hack it!

When we are trying to build a search bar in the home page, we might use Active Record Query Condition as follows (to search user emails that match the query).

Assume

{% highlight ruby %}
query = "Jack"
{% endhighlight %}

Action record query is

{% highlight ruby %}
User.where("name = '#{query}'")
{% endhighlight %}

Then it would return all users named **Jack**.

Though it works, a big security problem would hide behind it all the time unless we understand the SQL commands underneath.

{% highlight sql %}
SELECT * FROM users WHERE (name = 'Jack')
{% endhighlight %}

### SQL Injection

What if instead we change the query in search bar to

{% highlight ruby %}
query = "' OR name = 'Sarah"
{% endhighlight %}

Then SQL underneath would be

{% highlight sql %}
User.where("name = '' OR name = 'Sarah'")
{% endhighlight %}

Which would return user **Sarah**.

What if this is user authentication system instead of query system, then you could login as any user you want! That's dangerous!

### Solution

The solution is using `?` instead of interpolation.

{% highlight ruby %}
User.where("name = ?"), query
{% endhighlight %}
