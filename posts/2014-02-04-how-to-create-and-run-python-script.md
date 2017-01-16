---
layout: post
title: How to Create and Run Python Script
date: 2014-02-04 16:19:03
categories: Python
---

> How do I know if the Python code works? Wait! I don't even know how to run it!

### Here is the outline of the story

1. Install Python if you don't have one.
2. Create a python script file, let's start with `helloworld.py`.
3. Open and write `Hello World` codes in `helloworld.py`.
4. Run it!

### Step 1 : Install Python if you don't have one

In Unix like OS, you could easily install application via package management tool `apt-get`

{% highlight bash %}
# downloads and update the package lists from the repositories
sudo apt-get update
# install python 2.7
sudo apt-get install python2.7
{% endhighlight %}

Here, `sudo` is short for `superuser do`, which would run all the command as root.

### Step 2 : Create the python script file

Open Terminal and type in the following

{% highlight bash %}
# create `helloworld.py`
touch helloworld.py
{% endhighlight %}

Two basic things we learned here. First, `.py` is the python script file. Second, `touch` is what is commonly used to create an empty file.

### Step 3 : Open and write `Hello World` in the python script

There are several ways to open python script file `helloworld.py`, choose one of the following

{% highlight bash %}
#  Method 1: vi editor
vi helloworld.py   # the very basic way to open files
#  Method 2: nano editor
#     Please use "sudo apt-get install nano" before using "nano"
#     more popular and easier to use, highly recommended
nano helloworld.py
{% endhighlight %}

After open `helloworld.py`, type in codes as follows

{% highlight bash %}
#!/usr/bin/env python
print "Hello World" # python version is 2.7
{% endhighlight %}

Notice that `#!/usr/bin/env python` is necessary in Unix/Linux/OSX, because it indicate what interpreter to use by having a `#!` at the start of the first line. The starter would always confused by this lines.

Then exit nano text editor by `Ctrl+X`, and then type in `Y` to save.

### Step 4 : Time to run the code!

For Unix/Linux/OSX users, there are basically two ways to run the script. Here, method 2 is more widely used and recommended.

{% highlight bash %}
#  Method 1
python helloworld.py   # run script directly using python
#  Method 2
#  "+x" means changing file modes to make it executable
chmod +x helloworld.py
#  "./" means the current directory
./main.py
{% endhighlight %}

Then you could see `Hello World` in the command line.

Done.
