---
title: Attribute Selector
date: 2015-03-23T19:20:07+00:00
layout: post
categories: JavaScript
---

> Select any DOM elements as you want.

Assume we have 20 inputs of movies in a form

{% highlight html %}
... (input 1 - 17)
<input type="hidden" name="movie_name" value="ironman" data-id="18">
<input type="hidden" name="movie_name" value="the-avengers" data-id="19">
<input type="hidden" name="movie_name" value="spiderman" data-id="20">
{% endhighlight %}

#### 1. If we want to find movie `id = 20` (`data-id = 20`)

We could simply use jQuery attribute selector to find id exactly equals 20.

$("input[data-id='20']");

#### 2. If movie id is variable `movie_id`

Then we could use three strings instead of one as the command.

{% highlight javascript %}
var movie_id = 20;

$("input[data-id='" + movie_id + "']");
{% endhighlight %}

#### 3. If we want to find movie name containing substring `man`

{% highlight javascript %}
$("input[name*='man']");
{% endhighlight %}

Following are more attribute selector

| Attribute Selector | TypeFormat |
| ------------------ | ---------- |
| attribute Contains Selector | [name*="value"] |
| attribute Contains Word Selector | [name~="value"] |
| attribute Ends With Selector | [name$="value"] |
| attribute Equals Selector | [name="value"] |
| attribute Not Equal Selector | [name!="value"] |
| attribute Starts With Selector | [name^="value"] |
| has Attribute Selector | [name] |
