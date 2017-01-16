---
title: Find Events Attached on an Element
date: 2015-03-18T14:59:53+00:00
layout: post
categories: JavaScript
---

> Find actions hidden behind, directly from UI in Google Chrome.

Some page loads tons of JavaScript and messes you up when you want to find actions attached to just one specific DOM element.

Here is the solution: Simple UI based way to find what and where corresponding JavaScript is with `$._data()` method.

Assume we have following element in our page,

{% highlight html %}
<div class="greeting">hello</div>
{% endhighlight %}

And two actions (click + mouseover) have been attached to this element.

{% highlight javascript %}
$(".greeting").click(function(){ console.log("Hello")});
$(".greeting").mouseover(function(){ console.log("World")});
{% endhighlight %}

In order to know what have been attached, simply do following after `Inspect Element` in Google Chrome.

{% highlight javascript %}
$._data($(".greeting")[0], "events")
{% endhighlight %}

With the returned object, go to handler and right click to `Show Function Definition`, then you shall see code details and where it is.

![find binded events](/assets/images/2015/03/find-binded-events.jpg)

Done.
