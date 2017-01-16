---
title: Append Data to Form in Ajax
date: 2015-03-10T21:00:46+00:00
layout: post
categories: JavaScript
---

> Advanced things are usually customizable. So is Ajax.

### We usually pass data to Ajax in two ways

#### 1. Directly define data by key and values

{% highlight javascript %}
$.ajax({
    ...
    data: { id: 7 }
    ...
});
{% endhighlight %}

#### 2. Pass a form

{% highlight javascript %}
form = $("form").serialize();

$.ajax({
    ...
    data: form
    ...
});
{% endhighlight %}

### What if we want both?

**customized data + form**

Solution depends on if **customized data** is simple string or object like hash

#### Case 1: customized data is simple string

{% highlight javascript %}
form = $("form").serialize();

formAppendMoreData = form + "&id=7";

$.ajax({
    ...
    data: formAppendMoreData
    ...
});
{% endhighlight %}

#### Case 2: customized data is object like hash

Let's take hash for example, key point is we use `.serializeArray()` instead of `.serialize()`

{% highlight javascript %}
// return array of objects instead of string
form = $("form").serializeArray();

// reformat form string to hash
formHash = formToHash(form);

// hash to append to form
hashAppendToForm = {
    id: 7,
    name: { first: "Chen", last: "Huang" },
}

// append hash to form data
formHash["hashAppendToForm"] = hashAppendToForm

$.ajax({
    ...
    data: formHash
    ...
});

function formToHash(form){
    var formHash;

    $.each(form, function(index, obj){
        formHash[obj.name] = obj.value
    });

    return formHash;
}
{% endhighlight %}

Case 2 is a little bit more complicated than Case 1, while it could handle more complicated data type.
