---
title: Execute a Function Only When DOM Is Fully Loaded
date: 2014-10-23T18:28:37+00:00
layout: post
categories: JavaScript
---

> Stop, DOM! I am not ready yet!

As a JavaScript beginner, there is always the case when

### What we want is

After page is loaded, click on specific text on our page and it shows associated texts to console. The JavaScript/jQuery codes are

{% highlight javascript %}
$("#hello-world-text").click(printHelloWorld);

var printHelloWorld = function() {
  console.log("Hello World")
};
{% endhighlight %}

### However, what we get is

When page is loaded, texts shows in console immediately but we don't touch the mouse or keyboard.

**The answer is**

`.ready()` function

### What .ready() does is

specifying a function to execute when the DOM is fully loaded. And it has three equivalent syntaxes, and we prefer the third one

- `$(document).ready(handler)`
- `$().ready(handler)`
- `$(handler)`

Notice that **handler = anonymous_function + codes_to_execute** as follows

{% highlight javascript %}
$(function() {
  $("#hello-world-text").click(printHelloWorld);

  var printHelloWorld = function() {
    console.log("Hello World")
  };
});
{% endhighlight %}

To further refactoring the codes, we could move `printHelloWorld` function out of anonymous function

{% highlight javascript %}
$(function() {
  $("#hello-world-text").click(printHelloWorld);
});

var printHelloWorld = function() {
  console.log("Hello World")
};
{% endhighlight %}

Now everything works as you expected.
