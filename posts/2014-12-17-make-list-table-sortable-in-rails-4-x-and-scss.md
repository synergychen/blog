---
title: Make List / Table Sortable in Rails 4.x and SCSS
date: 2014-12-17T23:23:05+00:00
layout: post
categories: Ruby-On-Rails
---

> One step forward to better user experience.

![table sortable](/assets/images/2014/12/table-sortable.gif)

### Add jQuery rails gem

{% highlight ruby %}
gem 'jquery-ui-rails', '~>4.2'
{% endhighlight %}

### Require jQuery UI in JavaScript and SCSS

#### app/assets/javascripts/application.js

{% highlight javascript %}
//= require jquery.ui.all
{% endhighlight %}

#### app/assets/stylesheets/application.css.scss

{% highlight css %}
@import "jquery.ui.all";
{% endhighlight %}

### Enable jQuery Sortable Widget in JavaScript

Last step, using jQuery sortable widget to make list sortable

{% highlight javascript %}
$("ul").sortable();
{% endhighlight %}

or table sortable

{% highlight javascript %}
$("tbody").sortable();
{% endhighlight %}

To get more information about the dragged list or table row (In our demo case, **MIT** row)

{% highlight javascript %}
$("tbody").sortable().bind("sortupdate", function(event, ui) {
    console.log(ui.item);
});
{% endhighlight %}

Here `ui.item` would return jQuery object of **MIT** row.

You could see more about sortable widget in [jQuery UI API](http://api.jqueryui.com/sortable/).
