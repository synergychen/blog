---
title: How to Set Permanent and Temporary Alias in Unix
date: 2014-09-24T17:44:51+00:00
author: admin
layout: post
categories: Unix
---

> What's **alias**? A shortcut of a command.

If you type in the following commands in your terminal, the first would work and the second won't. However, we could make it happen for both in same function by setting **alias**. Setting **alias** is just like how we set variables, we need to find a place to make this two commands equals to each other, and such place is called **shell startup file**.

{% highlight bash %}
cd ~/Desktop
desk
{% endhighlight %}

### Shell Startup File

A shell startup file contain various system and user-defined variables and configurations that would be loaded in startup. alias is also be defined here.

If you are using bash, `~/.bashrc` is your shell startup file.

If you are using zsh, `~/.zshrc` is your shell startup file.

To check which shell you are using, do

{% highlight bash %}
which shell
{% endhighlight %}

Then we could edit the file and add our alias, here I use Vim for editing and my shell is zsh.

{% highlight bash %}
vim ~/.zshrc
{% endhighlight %}

### Set permanent alias (works after restart terminal or computer)

After in the editing view, simply add the follow command into your shell startup file. Your could name whatever you want, like **desktop**, and add as many aliases as you want. Notice that alias is case sensitive.

{% highlight bash %}
alias desk='cd ~/Desktop'
{% endhighlight %}

Save your file, and reload the shell script file or just restart the terminal to make alias works.

### Set temporary alias (won't work after restart terminal or computer)

There are bunch of times we just need the alias for today, we don't want to add them in the shell script file and delete it tomorrow, in such case, we could set temporary alias.

{% highlight bash %}
alias test='cd ~/Desktop/test'
{% endhighlight %}

To check what alias we currently have, just type in

{% highlight bash %}
alias
{% endhighlight %}

Done!
