---
title: Click to Edit Text Using JavaScript and Ajax
date: 2014-10-24T21:10:10+00:00
layout: post
categories: JavaScript
---

> Hack into the plain text!

![update text by javascript gif](/assets/images/2014/10/update-plain-text-using-javascript-gif.gif)


Making it look the same as plain text but act as a text field when editing. That's what we want to do. Before getting into JavaScript codes, we may first

### See how it works

1. (User) click on the text to edit
2. (JavaScript) change text from plain text to text field and make it editable
3. (User) type in new text
4. (User) press `Enter` key and (JavaScript) make text return to plain text

### Change it to our code/JavaScript Business Logic

![update text by javascript diagram](/assets/images/2014/10/update-plain-text-using-javascript-logic-diagram.jpg)

### Our .html.erb file is

{% highlight html %}
<li data-id="7">
  <p class="title">old-text</p>
</li>
{% endhighlight %}

### Our .js file is

{% highlight javascript %}
$(function() {
  $("body").on("click", ".title", editTaskTitle);
});

var editTaskTitle = function() {
  $(this).attr("contenteditable", true).focus();
  $(this).on("keydown", function(){
    if (event.keyCode === 13) {
      var newTaskTitle = $(this).text();
      var conversation = $.ajax({
          url: "/tasks/" + $(this).parent().data("id"),
          type: "PATCH",
          data: { task: { title: newTaskTitle }}
      });
      $(this).attr("contenteditable", false);
      return false;
    }
  });
};
{% endhighlight %}

### Some NOTES referring to .js file

**$(this)**

Returns jQuery object of class="title".

**.attr(attributeName, value)**

Change the attribute value of jQuery object. Create the attribute name and value if jQuery object doesn't have one.

**keyCode 13**

Refers to key `Enter`.

**.parent()**

Look one single level up the DOM tree.

**.data("id")**

Return value of DOM attribute `data-id`.

**Type in Ajax**

`PATCH` method is used in Ajax for updating data.

**Data in Ajax**

Assume we have a model task with column title. According to Rails, where the params is

{% highlight ruby %}
Parameters: {"task" => {"title" => "new"}, "id" => "7"}
{% endhighlight %}

In order to pass the right data to server using Ajax, we need to put title inside of another hash, just as

{% highlight ruby %}
data: {task: {title: newTaskTitle}}
{% endhighlight %}
