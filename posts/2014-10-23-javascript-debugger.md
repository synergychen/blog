---
title: JavaScript Debugger
date: 2014-10-23T18:31:25+00:00
layout: post
categories: JavaScript
---

> Code, debug and test. No one should left behind.

Debugging is interesting.

Thanks to chrome developer tool, we could do that pretty simple by adding `debugger;` in JavaScript, just as follows

The codes try to print `Hello` and `World` to console when we click on text with attribute `id="hello-world-text"`.

{% highlight javascript %}
$(function() {
  $("#hello-world-text").click(printHelloWorld);
});

var printHelloWorld = function() {
  console.log("Hello")
  debugger;
  console.log("World");
};
{% endhighlight %}

Then as we click the text, it would stop in debugger line. Then in console you could type in any JavaScript codes.
