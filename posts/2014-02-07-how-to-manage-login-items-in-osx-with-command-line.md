---
title: How to Manage Login Items in OSX with Command Line
date: 2014-02-07T13:59:14+00:00
layout: post
categories: MacOSX
---

> With command line, you could do everything.

### How to add login scripts?

In order to run scripts during the system startup, we could run the command in terminal

{% highlight bash %}
sudo defaults write com.apple.loginwindow LoginHook </path/to/script>
{% endhighlight %}

`com.apple.loginwindow` is the system login preference files (`.plist`) under `/Users/chenhuang/Library/Preferences/`. In Mac OSX, `.plist` is not readable with **vi** or **nano** editor since it is a binary file, while it could be opened with **Xcode** or **TextEdit**.

### How to look up the login items?

Unlike the login script hooks which reside in `com.apple.loginwindow.plist`, the login items/applications are in `com.apple.loginitems.plist`. To see the login items of the system, we could simply use `open -a` in terminal.

{% highlight bash %}
open -a Xcode /Users/chenhuang/Library/Preferences/com.apple.loginitems.plist
{% endhighlight %}

### How to add the login items?

Unlike adding login scripts, we use a different way to add login items **AppleScripts**(osascript command-line tool). Here, we add **TextEdit.app** as an example.

To add login items, in terminal do the followings

{% highlight bash %}
osascript -e 'tell application "System Events" to make new login item at end with properties {path:"/Applications/TextEdit.app", name:"TextEdit", hidden:true}'
{% endhighlight %}

The `hidden:true` would let the item hide after login.

To remove login item,

{% highlight bash %}
osascript -e 'tell application "System Events" to delete login item "TextEdit"'
{% endhighlight %}

To list all login items,

{% highlight bash %}
osascript -e 'tell application "System Events" to get the name of every login item'
{% endhighlight %}
