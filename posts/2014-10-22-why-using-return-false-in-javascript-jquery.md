---
title: 'Why Using return false in JavaScript / jQuery'
date: 2014-10-22 14:58:56
layout: post
categories: JavaScript
---

> return false: stop submitting the form!

What shall we do if we want to do something else other than submitting a form when clicking **submit** button? The answer is JavaScript/jQuery. However, sometimes we will still render another page after finishing our JavaScript tasks, and the solution is `return false` as follows

{% highlight javascript %}
$(function() {
  var newForm = $("form");
  newForm.submit(DoSomething);
});

function DoSomething() {
  // create a new form
  return false;
};
{% endhighlight %}

`return false` would stop submitting the form after you do something (such as create a new form) on clicking submit button.

Here are two failure cases when mis-using `return false`.

### Failure case 1

The common failure case is without `return false` to stop JavaScript.

{% highlight javascript %}
$(function() {
  var newForm = $("form");
  newForm.submit(DoSomething);
});

function DoSomething() {
  // create a new form
};
{% endhighlight %}

### Failure case 2

Another failure is using `return false` outside of submit action instead of inside. Same as failure case 1, this won't stop it to submit the form.

{% highlight javascript %}
$(function() {
  var newForm = $("form");
  newForm.submit(DoSomething);
  return false;
});

function DoSomething() {
  // create a new form
};
{% endhighlight %}
