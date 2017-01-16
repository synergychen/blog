---
title: Fast File Search and Content Replace in Unix
date: 2014-10-03T15:37:41+00:00
layout: post
categories: Unix
---

> This is how Unix boosts up your work.

This blog assumes your knowing about basic unix commands like `ls`, `cd`, and `/bin` is where these basic commands stay.

Here are some problems you might also have met or will meet:

### Find all files with a specific filename

If you want to return all the file names with specific pattern, use `find` or `ag` command

{% highlight bash %}
find <directory> -name <filename>
{% endhighlight %}

{% highlight bash %}
# find all files containing "resume" in file name: case sensitive
find . -name "*resume*"
# find all files containing "resume" in file name: case insensitive
find . -iname "*resume*"</pre>
{% endhighlight %}

{% highlight bash %}
ag -g <filename> <directory>
{% endhighlight %}

{% highlight bash %}
# the following three commands realize the same function
# ag is case insensitive
ag -g "resume" ./
# <directory> is default to be the current directory
ag -g "resume"
# double quote could be removed
ag -g controller
{% endhighlight %}

### Find all files containing specific content/text

If you want to return all the file names and matched lines with specific pattern, use `ag` command

{% highlight bash %}
ag <filename> <directory>
{% endhighlight %}

### Substitute old text with new text in a file

{% highlight bash %}
sed -i "" 's/<old_text>/<new_text>/g' <filename>
{% endhighlight %}
