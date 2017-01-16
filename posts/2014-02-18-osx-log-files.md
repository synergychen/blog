---
title: OSX Log Files
date: 2014-02-18 15:48:45
layout: post
categories: MacOSX
---

> The system has an eye on you. Want to see what he knows? Let's jailbreak into his mind logs.

### System Log

The system log locates in `/var/log/system.log`. The log would track the history of starting or restoring any applications, while it could not track when you close the applications. To see the realtime values of system log, you might use `tail` command.

{% highlight bash %}
tail -f /var/log/system.log
{% endhighlight %}

### Crash Log

The crash log in Lion/Mavericks usually stays in two places: `~/Library/Logs/CrashReporter/MobileDevice` and `~/Library/Logs/DiagnosticReports`. **CrashReporter** is used to report crash details such as stack traces, type of crash, and version of software, in Lion/Mavericks, it is used to monitor crash logs of your iOS devices if any. In order to monitor the system crash logs, it's easier to go to **DiagnosticReports**.

### Printing Log

The printing log stay in `/var/log/cups`, where `cups` is short for Common Unix Printing System and it could be found in Unix and OSX. In OSX, there are three files in this directory, `access_log`(connection history to printer), `error_log`(errors of connections) and `page_log`(printed file names and who has sent the tasks).
