---
title: Add Changes to Last Commit
date: 2014-10-13 15:19:25
layout: post
categories: Git
---

> I have just committed and soon realize that I forget to add something, but I don't want to do another commit.

Programmers sometimes forget to add some tiny change to the last commit, while they don't want to create another commit to declare little change. A easy way is using `reuse-message` in git.

{% highlight ruby %}
git commit --amend -C HEAD
{% endhighlight %}

`-C`: take an existing commit object, and reuse the log message and the authorship information (including the timestamp).
