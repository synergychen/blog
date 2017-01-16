---
title: How to Run Local Script on Remote Server via SSH
date: 2014-02-09T06:03:52+00:00
layout: post
categories: Unix
---

> Do everything in one command. That's why I love script.

### Old way : 3 commands

Sometimes we want to run a local script on a remote server via SSH, and usually what we do are

1. SSH login and type in passwordssh

{% highlight bash %}
<server_name>@<server_ip>
{% endhighlight %}

2. Use scp to transfer local script to remote server

{% highlight bash %}
scp </path/to/local_file> <server_name>@<server_ip>:</path/to/server>
{% endhighlight %}

3. Run script in remote server

{% highlight bash %}
./<script_name>
{% endhighlight %}

### New way : 1 command

And here is one command to put all three steps in one command

{% highlight bash %}
ssh <server_name>@<server_ip> < </path/to/script>
{% endhighlight %}

Here, `<` is used to input and run the script on server, </path/to/script> is the location of local script. Make sure `chmod +x` before you run the script, otherwise the script is not executable.

If you are tired of typing in password every time you use SSH, you could refer to [Goal 2: SSH without password](/ios/2014/02/04/how-to-ssh-and-transfer-files-between-mac-and-iphoneipad.html).
