---
layout: post
title: How to SSH and Transfer Files From/To iPhone/iPad
date: 2014-02-04 15:59:11
categories: iOS
---

> We use the iPhone charging&sync cable. It's not because we want to, but we have to. For those who hate cable/wire, I can help.

### What goals would we reach here?

1. SSH to iPhone/iPad and change password
2. SSH without password
3. Transfer file between Mac and iPhone/iPad

### What we need to prepare before starting?

1. [Have your iPhone/iPad jailbroken](http://evasi0n.com/)
2. Install &#8220;Open SSH&#8221; in Cydia

Notice that keeping your iPhone/iPad on during SSH.

### Goal 1: SSH to iPhone/iPad

1. Get the IP address of your iPhone/iPad
2. Open Terminal in Mac
3. Now ssh to iPhone/iPad and type in its password
4. Change SSH password

```bash
# SSH to iPhone/iPad
ssh root@<Your iPhone/iPad IP Address>
# Type in default password
alpine
# You are now logging in
# Now change the password
passwd
New password: <Your password>
Retype new password: <Your password again>
```

### Goal 2: SSH without password

1. Open Terminal
2. Creates the public and private keys

{% highlight bash %}
ssh-keygen -t rsa
{% endhighlight %}

Then you would see the followings line by line. Your need only type in `y` in
`Overwrite (y/n)? y`, for all the others, just press `Enter` to pass.
3. Copies the local-host's public key to the remote-host's authorized key file

{% highlight bash %}
ssh-copy-id root@<Your iPhone/iPad IP Address>
{% endhighlight %}

Now you could ssh to your iPhone/iPad without password.

### Goal 3: Transfer file between Mac and iPhone/iPad

Now we could use our Mac to access all the files in iPhone/iPad. For most of the
time, we are transferring files between Mac and iPhone/iPad, Here is "how to".

#### Transfer files from Mac to iPhone/iPad

{% highlight bash %}
# transfer a single file
scp </MacDir/FromFile> root@<iPhone IP>:</iPhoneDir/ToFile>
# transfer a folder
scp -r </FromMacDir> root@<iPhone IP>:</ToiPhoneDir>
{% endhighlight %}

#### Transfer files from iPhone/iPad to Mac
{% highlight bash %}
# transfer a single file
scp root@<iPhone IP>:</iPhoneDir/FromFile> </MacDir/ToFile>
# transfer a folder
scp -r root@<iPhone IP>:</FromiPhoneDir> </ToMacDir>
{% endhighlight %}
