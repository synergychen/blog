---
title: Detect When an Element is Inserted
date: 2015-04-16T22:50:13+00:00
layout: post
categories: JavaScript
---
> Sir, we got attack from enemy!!!

In the scene above, `we` and `enemy` stands for `DOM` and `inserted element`, respectively in Javascript.

Assume we have the following html, JavaScript

### world.html

{% highlight html %}
<div id="we"></div>
<div id="enemy"></div>
{% endhighlight %}

### alert.js

This is the function used to alert user when `DOM` is inserted to `we` div. Notice that `event.target` returns `inserted element`.

{% highlight javascript %}
$("#we").on("DOMNodeInserted", function(event) {
    var target = $(event.target).attr("id");

    alert(target + " is attacking us!!!");
});
{% endhighlight %}

### attack.js

Now if we insert `enemy` div into `we` div and we would get alert with attacking message.

{% highlight javascript %}
$("#we").append($("#enemy"));
{% endhighlight %}

![dom inserted notification](/assets/images/2015/04/dom-inserted-notification.jpg)
