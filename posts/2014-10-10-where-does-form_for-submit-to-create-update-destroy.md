---
#title: Where Does form_for Submit To – Create/Update/Destroy
date: 2014-10-10 15:48:31
layout: post
categories: Ruby-On-Rails
---

> Rails convention, again. However, everything goes for a reason.

Here is a typical **form_for** template, which provides you with a submit button on your website, but the question is, Which action/method will you call in controller? Create, submit or destroy? or just randomly?

{% highlight erb %}
<%= form_for @image do |form| %>
  ...
  <%= form.submit %>
<% end %>
{% endhighlight %}

The simple answer is **Rails convention**, while there is always a story behind that, and here is the story, of which the secret is `@image`.

When we pass `@image` to the form, Rails would go to the image controller in `app/controllers/images.rb` no matter where the form is.

### Submit to create action

If `@image = Image.new`, which means `@image` doesn't exist in database, then it would go to **create** action in image controller to create a new image.

### Submit to update action

If `@image = Image.find(params[:id])`, which means `@image` exists in database, then it would by default go to **update** action in image controller unless you specify delete method in the form.

### Submit to destroy action

As same as **update** action, `@image = Image.find(params[:id])`, then only if you specify the `method: :delete` in the form would it do destroy action. The form would be modified to

{% highlight erb %}
<%= form_for @image, method: :delete do |form| %>
  ...
  <%= form.submit %>
<% end %>
{% endhighlight %}

The whole decision making process in Rails is like following diagram

![where-does-form_for-submit-to](/assets/images/2014/10/where-does-form_for-submit-to.jpg)

Now you would never worry about where the submit would go. Randomly? Never!
