---
title: 'Immediately-Invoked Function Expression : Make Everything Private'
date: 2014-12-18T04:40:19+00:00
layout: post
categories: JavaScript
---

> By default, top level JavaScript variables and methods are global (public), unless you use Immediately-Invoked Function Expression(IIFE).

### Why using IIFE?

Make all variables and methods being private to avoid polluting the global namespace.

For example, we have two JavaScript files:

### a.js

{% highlight javascript %}
$(function() {
  var x = 0;
});
{% endhighlight %}

### b.js

{% highlight javascript %}
$(function() {
  var x = 1;
});
{% endhighlight %}

Then if you call variable `x` in anywhere else, it would return 0 or 1 depending on which JavaScript (a.js or b.js) is load first. It indicates that the top level variables and methods are public by default, thus global namespace is easily getting polluted.

### What does IIFE look like?

IIFE is basically wrapping your JavaScript with an anonymous function and directly call this function.

{% highlight javascript %}
(function() {
  // original JavaScript code here
})();
{% endhighlight %}

In our case for `a.js` (same case for `b.js`)

{% highlight javascript %}
(function() {
  $(function() {
    var x = 1;
  });
})();
{% endhighlight %}

### How it works?

IIFE would executes JavaScript code immediately as page is loaded.

Since IIFE would protect all variables and methods of JavaScript, in our case, `x` is no longer accessible outside of `a.js` and `b.js`, therefore, try accessing variable `x` would result in reference error instead of getting value of 0 or 1.

{% highlight javascript %}
Uncaught ReferenceError: x is not defined
{% endhighlight %}

### Recommendation of Using IIFE

Do use IIFE to wrap every JavaScript file.

If you are not sure if a method or variable should be private or public, make it private using IIFE!
