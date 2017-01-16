---
title: How to Install Software in Unix/Linux/OSX
date: 2014-02-04T16:23:57+00:00
layout: post
categories: Unix
---

> What's behind the commands ?

Thanks to developers for creating the advanced package tool. We might install most of the softwares with only one command, while sometimes we want to know more. Here we would mention two basic ways to install software in Unix like OS, and what's behind each command.

The mechanism of way 1 and way 2 are much the same, while way 1 is more easy and commonly used and recommended.

### Way 1: Using Packaging Tools

Here we choose two of the most popular packaging tools

#### [APT](http://en.wikipedia.org/wiki/Advanced_Packaging_Tool) (Linux)

{% highlight bash %}
# update the library before installing
sudo apt-get update
# install or uninstall software
sudo apt-get install/uninstall <software name>
{% endhighlight %}

Usually `apt-get` a build-in packaging tool for Linux, and it simplifies the process of managing software on Unix-like computer systems by automating the retrieval, configuration and installation of software packages, either from precompiled files or by compiling source code. Unfortunately, OSX is not supported for APT, but Homebrew could be a excellent substitution.

#### [Homebrew](http://brew.sh/) (OSX)

{% highlight bash %}
# update the library before installing
sudo brew update
# install or uninstall software
sudo brew install/uninstall <software name>
{% endhighlight %}

Homebrew is specific for OSX and it's quite clean and decent. And you could easily search for software using brew

{% highlight bash %}
sudo brew search <software name>
{% endhighlight %}

### Way 2: Compile and Install from source

The packaging tools (APT or Homebrew) could help you configure, compile and install the software you want with only one command, however, sometimes you may fail to find or install the software with the packaging tools, then you need to do everything by your own.

#### 1. Download the software package (.tgz, .tar.gz).

{% highlight bash %}
wget <website link>
{% endhighlight %}

Before compile and install the software, we need to download the software first. You could either download software with visiting the website or using the `wget` tool as follows

#### 2. Unzip the package

{% highlight bash %}
# use "man tar" to see the references of "xvzf"
tar xvzf <*.tgz or *.tar.gz>
{% endhighlight %}

#### 3. Check the details of you computer and generate **makefile**

{% highlight bash %}
./configure
{% endhighlight %}

This command is running the **configure** in your unzipped file, and it basically do two things. First, check and test the dependencies on the computer to see if everything that is needed works. If something is missing, the process would stop and you might need to google the problem and fix it based on the error report. If everything is OK, it would generate a file named **makefile**.

The **makefile** is extremely important, it contains various steps that are needed to be taken during compiling, which are the following steps.

#### 4. Compile all the program codes and create the executables

{% highlight bash %}
make
{% endhighlight %}

Since everything needed have already been check in `./configure`, here we only need to let the `make` utility to follow the steps in **makefile** to compile codes and create **executables**.

Notice that in some systems, `make` utility has not been built-in. To solve this problem, you may use one of the following commands

{% highlight bash %}
# Linux user sudo brew install build-essential # OSX user
sudo apt-get install build-essential
{% endhighlight %}

#### 5. Finish install

{% highlight bash %}
make install
{% endhighlight %}

`make install` let the `make` utility to search the `install` part in **makefile** and execute only that part. Before this step, all the files of the software are compiled and created in the temporary file, so other softwares could not use them. However, during this step, the required files would be copied into desired directory.

Done !
