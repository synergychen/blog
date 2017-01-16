---
title: 'jQuery Plugin &#8211; Add/Extend jQuery Functions'
date: 2015-04-01T00:05:00+00:00
layout: post
categories: JavaScript
---

> jQuery is powerful but not as much as you want. Therefore, complementing it.

Plugin is something we invent to enhance the function of original software/tool. For jQuery? Yes, we can.

### Add jQuery function

{% highlight javascript %}
$.fn.change_color = function(){
    $(this).css("color", "green");
};

$("#title").change_color();
{% endhighlight %}

### Add jQuery function with parameters

{% highlight javascript %}
$.fn.change_color = function(color){
    $(this).css("color", color);
};

$("#title").change_color("green");
{% endhighlight %}

### Add jQuery function with parameters + chaining

**Chaining** is one key feature of jQuery, so we don't want miss this feature when we defining our own jQuery function. Simply `return this` after defining jQuery function to keep this feature, similar to `return self` in Ruby.

{% highlight javascript %}
$.fn.change_color = function(color){
    $(this).css("color", color);
    return this;
};

$("#title").change_color("green").addClass("colorChanged");
{% endhighlight %}

### Add jQuery function with parameters + chaining + scope

In order to avoid namespace conflict between jQuery/javaScript library and user defined functions, we need to add `mmediately-Invoked Function Expression (IIFE)` to make your functions private. In this way, `change_color` method is inaccessable outside `(function(){...})();`.

{% highlight javascript %}
(function(){
    $.fn.change_color = function(color){
        $(this).css("color", color);
        return this;
    };
})();
{% endhighlight %}

### Add jQuery function with parameters + chaining + scope + extend more functions

jQuery provides `$.fn.extend()` method to make it easier if developers try to add more functions at one time.

{% highlight javascript %}
(function(){
    $.fn.extend({
        change_color: function(){
            ...
        },
        change_background: function(){
            ...
        }
    });
})();
{% endhighlight %}

### Extend existed jQuery function

{% highlight javascript %}
(function(){
    var oldCssFn = $.fn.css;

    $.fn.css = function(color){
        var originFn = oldCssFn.apply(this, arguments);

        // user defined function/behavior here
        alert("CSS has been Changed.")

        return originFn;
    };
})();
{% endhighlight %}
