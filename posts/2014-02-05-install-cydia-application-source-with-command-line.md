---
title: Install Cydia Application/Source with Command Line
date: 2014-02-05T04:42:56+00:00
layout: post
categories: iOS
---

> The fastest way to install Cydia application is using command line.

### Requirements

1. iOS jailbroken in your iPhone/iPad.
2. Setting to be a **Hacker** in Cydia.
You could set **Hacker** from `Cydia -> Manage -> Settings -> Hacker`. It allows you to use command line tools, which is restricted for **User**.
3. In Cydia, search and Install [Apt 0.7 Strict](http://modmyi.com/cydia/apt7 "Apt 0.7 Strict"), which is the advanced packaging tool from Debian to allow you using `apt-get`.
4. In Cydia, search and install [Open SSH](/ios/2014/02/04/how-to-ssh-and-transfer-files-between-mac-and-iphoneipad.html).

### Update and upgrade Cydia

Open terminal in your PC, then SSH to iPhone/iPad according to [How to SSH and Transfer Files From/To iPhone/iPad](/ios/2014/02/04/how-to-ssh-and-transfer-files-between-mac-and-iphoneipad.html)

Before adding any Cydia source or installing Cydia applications, it's recommended to update Cydia repositories and upgrade all Cydia changes. In terminal, type in the follows

{% highlight bash %}
#  update Cydia repositories
apt-get update
#  upgrade all Cydia changes
apt-get upgrade
{% endhighlight %}

Sometimes, you might get errors after update or upgrade as follows, and it usually occurs when some apt like terminal is running in your device. This problem could be solved by rebooting device.

{% highlight bash %}
Could not get lock /var/lib/dpkg/lock - open (35: Resource temporarily unavailable)
{% endhighlight %}

### Add Cydia source

The Cydia source is in `/etc/apt/sources.list.d/cydia.list`. If we want to add a source like `http://apt.weiphone.com`, for example, we could do

{% highlight bash %}
#  append source to Cydia source list
echo "deb http://apt.weiphone.com/ ./" >> /etc/apt/sources.list.d/cydia.list
#  refresh/update Cydia sources
apt-get update
{% endhighlight %}

### Install Cydia application

Take the application **FakeCarrier** for example, the corresponding website is `com.mirrordev.fakecarrier`. To install, do

{% highlight bash %}
# it is recommended to update and upgrade before installing any application
apt-get update
apt-get upgrade
#  install application
apt-get install com.mirrordev.fakecarrier
{% endhighlight %}

### Check installed applications/packages

{% highlight bash %}
# list all installed apps/packages
dpkg -l
{% endhighlight %}
