---
title: 'Solution: Stuck at OSX Login Window'
date: 2014-02-04 16:31:03
layout: post
categories: MacOSX
---

> What? I couldn't login OSX after type in my password!

**Problem Description**

I added a startup script (.sh) to the system in the following way

{% highlight bash %}
sudo defaults write com.apple.loginwindow LoginHook </path/to/script>
{% endhighlight %}

and restarted my Mac to test if it worked as I expected. Then I typed in the passwords as usual, but the problem was that the screen stopped at the login screen and never went to the desktop again.

### Cause Analysis

The reason is that the startup script has not been finished. The system would login to your desktop only when the startup script you added has been finished. For example, in my startup script, I had a **while** loop to get the IP address for every 10 minutes, but without a break in the loop as you can imagine. Therefore, the system would run the startup script forever and, of course, never would I be able to go to desktop.

### Solution

Regrets never solve problems. You must do something while it seems impossible, because you couldn't go to desktop, not to see command line or anything else. Luckily, Apple has left us a back door

1. Restart your computer and quickly press `Command + S` to start **Single-User Mode**, namely the command line.
2. Then type in two commands to remove your startup script. Or you might also fix problems like **while** loop in the script to make it functional.

{% highlight bash %}
# make the file writable
mount -uw /
# rm startup script</pre>
rm </path/to/script>
{% endhighlight %}

Notice that the default **Single-User Mode** is read-only, so in order to remove or change startup script, you need to use `mount -uw /` to make it writable.

{% highlight bash %}
# Reboot OSX
sudo reboot
{% endhighlight %}

Done!
