---
title: Redirect/Reload Page Using JavaScript
date: 2015-04-22T13:24:45+00:00
layout: post
categories: JavaScript
---
> Rails: "I am busy right now. Do redirect/reload yourself."
> JavaScript: "Me? How?"

Yes, you can. Mr. JavaScript.

### Redirect page

We could do `window.location.replace` or `window.location.href` to redirect a page, however difference is

`redirect`: won't create session history, thus `back button` would fail in this case;

`href`: would create session history like clicking a link on your page, so `back button` would still work.

{% highlight javascript %}
// = HTTP redirect
window.location.replace("http://www.google.com")
// = click a link
window.location.assign("http://www.google.com")
window.location.href = "http://www.google.com"
{% endhighlight %}

`window.location.href` could also used to get current url.

### Reload page

{% highlight javascript %}
window.location.reload(true)
{% endhighlight %}
