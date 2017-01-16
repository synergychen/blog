---
title: Page Specific JavaScript in Rails
date: 2014-12-20T16:41:14+00:00
layout: post
categories: Ruby-On-Rails/JavaScript
---

> Why all, all, all my JavaScripts are loaded when I open every, every, every single page in my Rails app. Even some JavaScripts have never been used!

### Why shall we load page specific JavaScript? And how?

Why? Short answer is avoiding JavaScript errors and making app running faster.

How? Short answer is using `content_for` in Rails.

Here is what happens underneath if we don't load page specific JavaScript.

Assume we have structure layout yield in application layout, and it points to three views/pages: index, new and show. As we require whole JavaScript folder in `application.js`, all JS file would be loaded for every view/page as shown below, which lead to a question: **Why do we need new.js and show.js for index view/page? Yes, we don't.**

![page specific javascript before](/assets/images/2014/12/page-specific-javascript-before.jpg)

### Solution: content_for

The content_for method allows you to insert content into a named yield block in your layout.

![page specific javascript after](/assets/images/2014/12/page-specific-javascript-after.jpg)

#### applicaiton.js

{% highlight html %}
<head>
  <%= yield "scripts" %>
</head>

<body>
  <%= yield %>
</body>
{% endhighlight %}

#### index.html.erb (same for show and new view)

{% highlight ruby %}
<%= content_for :scripts do %>
  <%= javascript_include_tag "index.js" %>
<% end %>
{% endhighlight %}

If you don't know which JS have been loaded for the current page, open Chrome DevTool and do as follows

![page specific javascript chrome debugger](/assets/images/2014/12/page-specific-javascript-chrome-debugger.gif)
