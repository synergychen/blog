---
title: Pass Checkbox Values as Array of Additional Model Objects to Controller
date: 2015-03-11T19:56:17+00:00
layout: post
categories: Ruby-On-Rails
---

> You could select multiple checkbox now.

Assume in `form_for` for `@person`, if you want select some additional model objects from `@floors`, you could do the following

#### 1. `fields_for` inside `form_for` to access additional model objects

{% highlight ruby %}
<!-- @person = Person.first -->
<= form_for @person do |form| >
    ...

    <= fields_for "apartments" do |field| >
    < end >

    ...
< end >
{% endhighlight %}

This would allow you access `params[:apartments]` in `persons_controller`

#### 2. `collection_check_boxes` to select multiple objects

{% highlight ruby %}
<!-- @person = Person.first -->
<!-- @floors = Floor.all -->
<= form_for @person do |form| >
    ...

    <= fields_for "apartments" do |field| >
        <!-- id : value passed to controller -->
        <!-- name : attribute displayed as label of check box -->
        <= field.collection_check_boxes "floor_ids", @floors, :id, :name >
    < end >

    ....
< end >
{% endhighlight %}

By doing second step, in `edit` action in `persons_controller`, you should be able to access params (assume we select id: `1`, `3`, `7`)

{% highlight ruby %}
params[:apartments][:floor_ids]
#=> ["1", "3", "7", ""]
{% endhighlight %}

Notice that params array ends with an empty string, and we usually need to handle it in controller to avoid possible errors.

#### 3. make `checkbox` and `checkbox_label` in same line

Up to now, `checkbox` works and `params` get passed. But, wait. Why `checkbox` and `label` are not displayed in same line? In order to solve this issue, we need to expand `collection_check_boxes` by doing:

{% highlight ruby %}
<!-- @person = Person.first -->
<!-- @floors = Floor.all -->
<= form_for @person do |form| >
    ...

    <= fields_for "apartments" do |field| >
        <!-- id : value passed to controller -->
        <!-- name : attribute displayed as label of check box -->
        <= field.collection_check_boxes("floor_ids", @floors, :id, :name) do |b| >
            <= b.label(class: "checkbox_label") do >
                <= b.check_box(class: "checkbox_box") >
                <= b.object.name >
            < end >
        < end >
    < end >

    ...
< end >
{% endhighlight %}

Checkbox and label are in same line now! You could also further purify css with the class given above(`checkbox_label` and `checkbox_box` in this case).
